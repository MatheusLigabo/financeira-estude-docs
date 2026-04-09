# Checklist de Performance e Resiliência Backend (Deep Dive)

Junior, no .NET, performance não é apenas "rodar rápido", é **eficiência de recursos**. Se você trava uma thread esperando o banco, você está jogando dinheiro fora e limitando o número de usuários do FinanceiraEstude.

---

## 🧠 1. Anatomia do Async/Await: A Máquina de Estados
Quando você usa `async/await`, o compilador do C# cria uma **Máquina de Estados**. 
- **O que acontece:** O método é fatiado. Quando ele bate no `await`, a thread atual é devolvida para o **Thread Pool** para atender outras requisições. Quando a tarefa termina, uma thread (pode ser a mesma ou outra) volta para continuar o código.

### **Transcrição Técnica: O Thread Pool**
> "O Thread Pool do .NET gerencia um conjunto de threads de trabalho. Quando uma thread termina sua tarefa, ela volta para a fila em vez de ser destruída. Isso evita o custo de criação de novas threads (que é caro)." 
> *Ref: Documentação Microsoft (Runtime)*

### **⚠️ Perigo: Thread Pool Starvation**
Se você usar `.Result` ou `.Wait()`, você trava uma thread do pool. Se muitas requisições fizerem isso, o pool esvazia e sua API para de responder (`HTTP 503 Service Unavailable`). **Regra de Ouro: Async até o topo!**

---

## 🛡️ 2. Resiliência: O Padrão Polly
Em sistemas reais, a rede falha. O banco de dados pode oscilar. O FinanceiraEstude deve ser um "tanque de guerra".

### **Estratégia 1: Retry (Retentativa)**
Se falhou uma vez, tente de novo após 2 segundos. Talvez tenha sido apenas um "soluço" na rede.
```csharp
// Transcrição de Uso (Polly):
var policy = Policy
    .Handle<SqlException>()
    .WaitAndRetryAsync(3, retryAttempt => TimeSpan.FromSeconds(Math.Pow(2, retryAttempt)));
```

### **Estratégia 2: Circuit Breaker (Disjuntor)**
Se o banco de dados falhou 10 vezes seguidas, não adianta tentar a 11ª. O "Disjuntor" abre e bloqueia todas as chamadas por 30 segundos para o banco respirar.
*Por que usar?* Para evitar o efeito cascata onde um erro em um serviço derruba todo o ecossistema.

---

## 🛑 3. Exception Handling (Gerenciamento Global)
Junior, nunca coloque `try/catch` em todos os métodos. Isso polui o código.
- **O Caminho Profissional:** Use um **Middleware Global de Exceção**. 
- **O Fluxo:** Se um erro acontecer em qualquer lugar (Domain, Application ou Infra), o Middleware captura, gera um Log detalhado para o Dev e retorna um JSON amigável para o usuário.

---

## 🏗️ 8 Exemplos Práticos de Performance e Resiliência

### 🚀 Exemplo 1: ConfigureAwait(false) - O "Libertador"
Sempre use em bibliotecas e camadas de Infra/Application.
```csharp
await _context.Aportes.ToListAsync().ConfigureAwait(false);
// Isso avisa: "Não preciso voltar para o contexto original, qualquer thread serve".
```

### 🚀 Exemplo 2: CancellationToken em Consultas Longas
```csharp
public async Task<List<Aporte>> Listar(CancellationToken ct) {
    // Se o usuário cancelar no navegador, o SQL para na hora!
    return await _context.Aportes.ToListAsync(ct);
}
```

### 🚀 Exemplo 3: IAsyncEnumerable (Streaming de Dados)
Se você tem 1 milhão de registros, não dê `.ToList()`. Use `IAsyncEnumerable`.
```csharp
public async IAsyncEnumerable<Aporte> GetStreaming([EnumeratorCancellation] CancellationToken ct) {
    foreach (var aporte in _context.Aportes.AsAsyncEnumerable()) {
        yield return aporte; // Envia um por um conforme o banco responde.
    }
}
```

### 🚀 Exemplo 4: Singleton para HttpClient
**Nunca** dê `new HttpClient()` dentro de um loop. Isso causa **Socket Exhaustion**. Use `IHttpClientFactory`.
*Ref Microsoft:* "HttpClient é projetado para ser instanciado uma vez e reutilizado."

### 🚀 Exemplo 5: Otimização de EF Core (`AsNoTracking`)
Para consultas de apenas leitura (Gráficos do FinanceiraEstude), use `.AsNoTracking()`. 
```csharp
var dados = await _context.Aportes.AsNoTracking().ToListAsync();
// O EF Core não vai "vigiar" esses objetos, economizando memória e CPU.
```

### 🚀 Exemplo 6: Global Exception Middleware
```csharp
public async Task InvokeAsync(HttpContext context) {
    try {
        await _next(context);
    } catch (Exception ex) {
        // Logue o erro REAL aqui (Serilog/Insights)
        await HandleExceptionAsync(context, ex);
    }
}
```

### 🚀 Exemplo 7: Cache com IMemoryCache
Evite ir no banco para dados que mudam pouco (ex: lista de Bancos ou Moedas).
```csharp
_memoryCache.GetOrCreate("moedas", entry => {
    entry.AbsoluteExpirationRelativeToNow = TimeSpan.FromHours(1);
    return _repo.GetMoedas();
});
```

### 🚀 Exemplo 8: Resiliência com Polly (Retry + Timeout)
Combine políticas. Se o serviço externo demorar mais de 5 segundos, cancele e tente de novo.

---

## 👨‍💻 Visão Sênior: O custo da invisibilidade
Junior, o pior erro é o "Silêncio do Erro". Se uma Exception acontece e você não tem log, você é cego. No FinanceiraEstude, cada falha deve ser rastreável. Use **Logs Estruturados** (JSON) para que possamos filtrar por `AporteId` ou `UsuarioId` em segundos.

*Documentação Essencial Transcrita:*
- **Async In-Depth:** O .NET usa o `SynchronizationContext` para gerenciar threads. No ASP.NET Core, esse contexto é `null` por padrão, o que facilita o uso de `async`, mas o `ConfigureAwait(false)` continua sendo uma boa prática de "higiene de código".

---

## 💡 Próximos Passos
Teste a resiliência do seu código:
[[Performance - Exercícios]]




