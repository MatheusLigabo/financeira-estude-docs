# Módulo 01: Domain-Driven Design (DDD) Profundo

O DDD não é sobre organizar pastas, mas sobre garantir que o código reflita exatamente a operação real da empresa (**Linguagem Onipresente**). No FinanceiraEstude, isso significa que um "Aporte" no código deve se comportar exatamente como um "Aporte" no mundo financeiro.

## 🧠 1. Os Blocos de Construção do Domínio

### **Entidades (Entities)**
- **O que são:** Objetos que possuem uma **Identidade Única** que persiste ao longo do tempo.
- **Exemplo:** Um `Aporte`. Mesmo que o valor mude (por um erro de correção), ele continua sendo o "Aporte ID 123".
- **DICA SÊNIOR:** No DDD, a Entidade deve se auto-validar. Se você criar um `new Aporte(-100)`, a entidade deve lançar uma exceção **imediatamente**.

### **Objetos de Valor (Value Objects)**
- **O que são:** Objetos definidos apenas por seus atributos. Eles não têm identidade.
- **Exemplo:** `Dinheiro` (Valor + Moeda). Se eu trocar uma nota de 10 reais por outra nota de 10 reais, você não se importa, porque o valor é o mesmo.
- **Vantagem:** Eles são **imutáveis**. Você nunca muda um Valor de Objeto; você cria um novo.

### **Agregados (Aggregates)**
- **O que são:** Um grupo de objetos (Entidades + VOs) que são tratados como uma unidade única para mudança de dados.
- **Raiz do Agregado (Aggregate Root):** É o único objeto do grupo que pode ser acessado de fora. No FinanceiraEstude, o `Aporte` é a raiz. Você não altera um "Item" do aporte sem passar pelo objeto `Aporte`.

## 🎼 2. Camada de Aplicação (Use Cases)
O Use Case é o "Maestro". Ele não sabe *como* salvar no banco, ele apenas coordena:
1. Recebe os dados da API (Request).
2. Busca a Entidade no Repositório.
3. Chama um método de negócio na Entidade (ex: `aporte.Processar()`).
4. Salva a Entidade de volta no Repositório.
5. Notifica a fila (RabbitMQ).

---

## 🏗️ 8 Exemplos Práticos de DDD no FinanceiraEstude

### 🗡️ Exemplo 1: O Construtor Blindado
```csharp
public class Aporte {
    public Aporte(decimal valor, DateTime data) {
        if (valor <= 0) throw new DomainException("Valor inválido.");
        if (data > DateTime.Now) throw new DomainException("Data futura não permitida.");
        
        Id = Guid.NewGuid();
        Valor = valor;
        Data = data;
    }
}
```

### 🗡️ Exemplo 2: Value Object 'Dinheiro'
```csharp
public record Dinheiro(decimal Valor, string Moeda) {
    public Dinheiro Somar(Dinheiro outro) {
        if (this.Moeda != outro.Moeda) throw new Exception("Moedas diferentes!");
        return new Dinheiro(this.Valor + outro.Valor, this.Moeda);
    }
}
```

### 🗡️ Exemplo 3: Encapsulamento de Lista
```csharp
private readonly List<Historico> _historico = new();
// Quem está fora só LÊ a lista, não pode dar .Add() ou .Clear()
public IReadOnlyCollection<Historico> Historico => _historico.AsReadOnly();

public void RegistrarMudanca(string motivo) {
    _historico.Add(new Historico(motivo));
}
```

### 🗡️ Exemplo 4: Bounded Contexts (Contextos Delimitados)
Não tente fazer um único `Usuario`. No contexto de **Login**, ele tem Senha. No contexto de **Aportes**, ele é apenas um `DonoDoAporte` com Nome e Email.

### 🗡️ Exemplo 5: Inversão de Dependência no Repositório
O Domínio define a interface. A Infraestrutura implementa.
```csharp
// No DOMÍNIO:
public interface IAporteRepository {
    Task AddAsync(Aporte aporte);
}
```

### 🗡️ Exemplo 6: Factory (Fábrica)
Se a criação de um `Aporte` for muito complexa (envolvendo taxas, conversão de moeda), use uma classe `AporteFactory` para centralizar a lógica de criação.

### 🗡️ Exemplo 7: Domain Events (Eventos de Domínio)
Quando um aporte é criado, a Entidade dispara um evento: `AporteCriadoEvent`. O sistema pode então enviar um e-mail sem que a Entidade saiba *como* enviar e-mail.

### 🗡️ Exemplo 8: Domain Services
Se uma regra de negócio envolver duas ou mais Entidades (ex: Transferir entre Carteiras), e a regra não "cabe" em nenhuma delas, crie um `TransferenciaService` no Domínio.

---

## 👨‍💻 Visão Sênior: O Perigo da "Pasta-Driven Development"
Junior, muitos acham que DDD é criar pastas como `Domain`, `Services`, `Repositories`. Isso é mentira. O DDD é sobre **Lógica de Negócio Protegida**. Se eu conseguir mudar o saldo de uma conta sem passar por uma validação, seu DDD falhou, não importa quão bonitas estão as pastas.

*Documentação Essencial:* [Livro de Bolso do DDD (Vernon)](https://dddcommunity.org/learning-ddd/books/)

---

## 💡 Próximos Passos
Treine seu cérebro para pensar em Regras de Negócio:
[[DDD - Exercícios]]


