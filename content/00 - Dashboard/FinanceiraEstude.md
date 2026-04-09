# 🏛️ FinanceiraEstude - Especificação Técnica e Arquitetura

## 📌 1. Visão Geral e Intuito
O **FinanceiraEstude** é um ecossistema de back-end focado na automação e organização de fluxos financeiros pessoais. O objetivo central é receber entradas de capital (Aportes), aplicar rigorosas validações de negócio e distribuir o processamento dessas informações de forma assíncrona, garantindo escalabilidade e resiliência.

**Objetivos Principais:**
- Centralizar o controle de entrada de dinheiro.
- Proteger as regras de negócio contra dados inválidos.
- Preparar o terreno para cálculos de rendimentos e integrações com "Caixinhas" no futuro.

---

## 🛠️ 2. Stack Tecnológico
- **Linguagem:** C# (.NET Core)
- **Arquitetura:** Clean Architecture + Domain-Driven Design (DDD)
- **Banco de Dados (Previsto):** PostgreSQL
- **ORM:** Entity Framework Core
- **Mensageria (Fila):** RabbitMQ
- **Documentação de API:** Swagger / OpenAPI

---

## 🏗️ 3. Camadas da Arquitetura (Clean Architecture)

O projeto foi rigorosamente dividido para garantir o **Princípio da Inversão de Dependência**. A regra fundamental é: as camadas externas (Banco, Internet) dependem do Domínio, mas o Domínio não depende de ninguém.

### 🫀 Domain (`FinanceiraEstude.Domain`) -> *O Coração*
É o centro do sistema. Não tem conhecimento de bancos de dados ou APIs.
- **AggregatesModel:** Agrupa entidades que pertencem ao mesmo contexto. 
  - Ex: `AporteAggregate` contém a Entidade Rica `Aporte.cs`.
- **Regras de Negócio (Fail-Fast):** A própria entidade se valida ao nascer (ex: construtor do Aporte lança erro se o valor for <= 0).
- **Interfaces (Contratos):** Define o que o sistema exige. 
  - Ex: `IAporteRepository` avisa que o sistema precisará salvar o aporte, mas não diz "como".

### 🎼 Application (`FinanceiraEstude.Application`) -> *O Maestro*
É a camada de orquestração. Não possui regras financeiras, apenas o roteiro de execução.
- **UseCases:** Organizados por funcionalidades (ex: pasta `Aportes` -> `RealizarAporteUseCase.cs`).
- **Responsabilidade:** Receber o pedido da API, instanciar a Entidade (que se auto-valida) e chamar o repositório para salvar no banco e notificar a fila.
- **Injeção de Dependência:** Solicita o `IAporteRepository` via construtor, sem saber qual tecnologia está rodando por trás.

### 🦾 Infrastructure (`FinanceiraEstude.Infrastructure`) -> *Os Braços (Trabalho Sujo)*
É quem lida com o mundo exterior (tecnologia de fato).
- **Repositories:** Classes que assinam os contratos do Domínio. 
  - Ex: `AporteRepository.cs` assina a interface e executa o `Insert` real no PostgreSQL usando o Entity Framework.

### 🛎️ API (`FinanceiraEstude.API`) -> *O Balcão de Atendimento*
A porta de entrada da internet.
- **Controllers:** Recebem as requisições HTTP (`POST`, `GET`). 
  - Ex: `AportesController.cs`.
- **DTOs:** Classes "burras" de transporte de dados (ex: `AporteRequest`), usadas apenas para ler o JSON que vem da internet.
- Captura exceções do Domínio (Regras de Negócio) e as transforma em respostas limpas (Status 400 Bad Request).

### 🤖 Worker (`FinanceiraEstude.Worker`) -> *O Robô Operário*
Serviço que roda em background 24/7.
- Fica "escutando" as filas do RabbitMQ.
- Quando um aporte é salvo, o Worker recebe a notificação e pode fazer processamentos pesados (enviar e-mail, calcular juros, gerar logs) sem deixar a tela do usuário travada carregando.

---

## 🔄 4. Ciclo de Vida de um Aporte (Data Flow)

Quando o usuário clica em "Salvar Aporte" (ou via Swagger), o fluxo exato é:

1. **[HTTP POST]** O JSON de entrada bate no `AportesController` (API).
2. **[Orquestração]** O Controller passa o valor cru para o `RealizarAporteUseCase` (Application).
3. **[Validação]** O UseCase tenta criar um `new Aporte()`. Se o valor for inválido, a entidade "grita" um erro que sobe de volta para o Controller.
4. **[Persistência]** Se válido, o UseCase chama o método `AdicionarAsync` do repositório injetado.
5. **[Banco de Dados]** O `AporteRepository` (Infrastructure) converte isso em SQL e salva no PostgreSQL.
6. **[Retorno]** A API responde **200 OK** para o cliente.

---

## 📂 5. Mapa de Estrutura de Pastas (Visual Studio)

```text
📁 FinanceiraEstude (Solução)
├── 📁 FinanceiraEstude.API
│   ├── 📁 Controllers
│   │   └── AportesController.cs
│   ├── appsettings.json
│   └── Program.cs (Injeção de Dependência e Swagger)
│
├── 📁 FinanceiraEstude.Application
│   └── 📁 UseCases
│       └── 📁 Aportes
│           └── RealizarAporteUseCase.cs
│
├── 📁 FinanceiraEstude.Domain
│   └── 📁 AggregatesModel
│       └── 📁 AporteAggregate
│           ├── Aporte.cs
│           └── IAporteRepository.cs
│
├── 📁 FinanceiraEstude.Infrastructure
│   └── 📁 Repositories
│       └── AporteRepository.cs
│
└── 📁 FinanceiraEstude.Worker
    └── Worker.cs


