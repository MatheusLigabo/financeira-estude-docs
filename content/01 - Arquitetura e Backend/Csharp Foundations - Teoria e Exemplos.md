# Módulo 00: C# Foundations - O DNA do FinanceiraEstude

Junior, para você construir o FinanceiraEstude, você precisa parar de ver o C# como um texto e começar a vê-lo como **gestão de recursos**. Aqui está tudo o que você precisa para sair do zero e chegar à maturidade técnica.

## 🧠 1. Gerenciamento de Memória e Ciclo de Vida
O .NET roda sobre a **CLR (Common Language Runtime)**. Quando você aperta "Play", seu código C# é compilado para **IL (Intermediate Language)** e depois o **JIT (Just-In-Time)** transforma isso em código de máquina.

### **Onde os dados moram?**
- **Stack (Pilha):** Imagine uma pilha de pratos. O último que entra é o primeiro que sai. É aqui que moram os **Value Types** (`int`, `decimal`, `bool`, `struct`, `Guid`). É ultra rápida porque o tamanho é fixo e conhecido.
- **Heap (Monte):** É um grande galpão bagunçado gerenciado pelo **Garbage Collector (GC)**. É aqui que moram os **Reference Types** (`class`, `string`, `List<T>`). O objeto fica lá enquanto houver uma "seta" (referência) apontando para ele na Stack.
- **DICA SÊNIOR:** Se você criar uma `List<Aporte>` com 1 milhão de itens, você está enchendo o Heap. Se você não limpar as referências, terá um **Memory Leak**.

## 🚀 2. Injeção de Dependência (DI): O Coração do .NET
O FinanceiraEstude usa DI em tudo. Em vez de você dar `new AporteRepository()`, você pede ao .NET: "Ei, me dá quem quer que implemente `IAporteRepository`".
- **Transient:** Criado toda vez que é pedido.
- **Scoped:** Criado uma vez por requisição HTTP (O padrão para Repositórios e Banco de Dados).
- **Singleton:** Criado uma única vez enquanto o app estiver ligado (Cuidado: pode causar bugs de estado compartilhado).

## 🛡️ 3. LINQ e Coleções (A Manipulação de Dados)
O LINQ (`System.Linq`) é a ferramenta mais poderosa do C#.
- **Deferred Execution:** O LINQ cria um "plano de busca". Ele só vai ao banco ou processa a lista quando você chama `.ToList()`, `.First()` ou um `foreach`.
- **IEnumerable vs List:** `IEnumerable` é apenas um "leitor" (não permite adicionar itens). `List` é a coleção real na memória. No FinanceiraEstude, retorne `IEnumerable` nas interfaces para proteger sua lista de ser alterada por quem não deve.

---

## 🏗️ 8 Exemplos Práticos Detalhados

### 💰 Exemplo 1: Por que 'decimal' e não 'float'?
```csharp
// FLOAT (Binário - Aproximado):
float f = 0.1f + 0.2f; // Resultado: 0.30000001 (Você perdeu dinheiro!)
// DECIMAL (Base 10 - Exato):
decimal d = 0.1m + 0.2m; // Resultado: 0.3 (Perfeito para o FinanceiraEstude)
```

### 🛡️ Exemplo 2: Null Safety (Evitando o erro bilionário)
```csharp
string? nome = null; // O '?' avisa que pode ser nulo.
int tamanho = nome?.Length ?? 0; // Se for nulo, retorna 0. Sem erro!
```

### 📋 Exemplo 3: Listas vs Dicionários (Performance)
```csharp
// Se você tem 10.000 aportes e quer buscar pelo ID:
// LISTA: Ele lê um por um até achar. (Lento!)
// DICIONÁRIO: Ele vai direto na "gaveta" certa pelo ID. (Instantâneo!)
var buscaRapida = dicionarioAportes[idProcurado];
```

### 🔄 Exemplo 4: Record para DTOs (Imutabilidade)
```csharp
// Use record para dados que viajam entre camadas. Eles são leves e seguros.
public record AporteRequest(decimal Valor, string Descricao);
```

### 🧪 Exemplo 5: O Try/Catch Correto
```csharp
try {
    RealizarAporte();
} catch (DomainException ex) {
    // Pegue erros específicos que você conhece.
    _logger.LogWarning(ex.Message);
} catch (Exception ex) {
    // Erros genéricos: Logue o erro REAL e lance de novo. Nunca engula o erro!
    _logger.LogError(ex, "Erro fatal no aporte");
    throw; 
}
```

### 🕵️ Exemplo 6: LINQ com Projeção (Anônimos)
```csharp
// Pegue apenas o que precisa para economizar memória:
var nomesEValores = aportes
    .Where(a => a.Valor > 100)
    .Select(a => new { a.Nome, a.Valor });
```

### 🏗️ Exemplo 7: Interfaces vs Classes Abstratas
- **Interface (`IAporte`):** É um contrato. "O que eu faço". (Ex: Salvar, Deletar).
- **Classe Abstrata (`BaseEntity`):** É um molde. "O que eu sou". (Ex: Todo objeto tem um Id e uma DataCriacao).

### 🚀 Exemplo 8: Task.WhenAll (Concorrência)
```csharp
// Se precisar buscar dados de 3 APIs diferentes:
var t1 = GetDolar();
var t2 = GetEuro();
var t3 = GetAportes();
await Task.WhenAll(t1, t2, t3); // As 3 rodam ao mesmo tempo. 3x mais rápido!
```

---

## 👨‍💻 Visão Sênior: O Caminho da Maestria
Junior, o compilador é seu professor mais rigoroso. Se ele deu erro, **leia o erro**. 90% dos seus problemas nos primeiros meses serão resolvidos lendo a mensagem de erro com calma. Não tente "chutar" o código até funcionar. Entenda o porquê de cada linha.

*Documentação Essencial:* [C# Fundamentos da Microsoft](https://learn.microsoft.com/pt-br/dotnet/csharp/)

---

## 💡 Próximos Passos
Vá para o laboratório e sinta a memória funcionando:
🔗 **[Abrir Laboratório de Fundamentos no VS Code](vscode://file/C:/Users/mtsli/OneDrive/%C3%81rea%20de%20Trabalho/Futuro/FinanceiraEstude/FinanceiraEstude/Exercises/Foundations/Fundamentos_Csharp.cs)**




