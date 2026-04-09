# 🗺️ FinanceiraEstude - Roadmap de Implementação

Este roteiro é o seu guia prático para aplicar cada módulo do Dashboard diretamente no projeto **FinanceiraEstude**. Siga estas fases para elevar o nível técnico do seu código.

---

## 🏗️ FASE 1: O Domínio Blindado (DDD)
*Objetivo: Garantir que as regras de negócio nunca sejam corrompidas.*

- [ ] **Task 1: Encapsulamento de Aportes.**
  - No arquivo `FinanceiraEstude.Domain/AggregatesModel/AporteAggregate/Aporte.cs`, garanta que **nenhuma** propriedade tenha `set` público.
  - Crie um construtor que valide se o valor é maior que zero.
- [ ] **Task 2: Objetos de Valor (Value Objects).**
  - Refatore o campo `Valor` para usar um record `Dinheiro(decimal Valor, string Moeda)`.
- [ ] **Lição de Apoio:** [[DDD - Teoria e Exemplos]]

---

## 🛢️ FASE 2: Persistência e Segurança (SQL)
*Objetivo: Gravar dados com performance e sem riscos de injeção.*

- [ ] **Task 1: Repositório Assíncrono.**
  - Implemente o `AporteRepository` usando `Dapper` ou `EF Core`.
  - Use sempre **Parâmetros Nomeados** nas queries SQL.
- [ ] **Task 2: Paginação de Aportes.**
  - Crie um método de listagem que aceite `Skip` e `Take` para não travar o banco ao carregar milhares de registros.
- [ ] **Lição de Apoio:** [[Mestre do SQL - Teoria e Exemplos]]

---

## 🚀 FASE 3: O Tanque de Guerra (Performance)
*Objetivo: API escalável que não trava threads.*

- [ ] **Task 1: Async até o topo.**
  - Garanta que todos os métodos da Controller e do Use Case usem `Task` e `await`.
- [ ] **Task 2: Resiliência com CancellationToken.**
  - Repasse o `CancellationToken` da API até a chamada final do banco de dados.
- [ ] **Lição de Apoio:** [[Performance - Teoria e Exemplos]]

---

## 🤖 FASE 4: Processamento Assíncrono (Worker)
*Objetivo: Tirar o peso das tarefas demoradas da tela do usuário.*

- [ ] **Task 1: Notificação de Sucesso.**
  - Após salvar um aporte, envie uma mensagem para o RabbitMQ.
- [ ] **Task 2: O Worker Operário.**
  - Configure o `FinanceiraEstude.Worker` para ler essa mensagem e simular o envio de um e-mail de confirmação.
- [ ] **Lição de Apoio:** [[SIMULADOR_DE_CAOS]] (Bloco 5).

---

## 🎨 FASE 5: A Vitrine (Frontend)
*Objetivo: UI fluida e sincronizada com a URL.*

- [ ] **Task 1: Filtros de Busca.**
  - Implemente a busca de aportes sincronizando o input com os **Query Params** da URL.
- [ ] **Lição de Apoio:** [[Gerenciamento de Estado - Teoria e Exemplos]]

---
> 👨‍💻 **Conselho do Mentor:** Não tente fazer tudo no mesmo dia. Escolha uma Task, revise a teoria no Dashboard, e só então abra o VS Code. A qualidade da sua entrega diz quem você é como desenvolvedor.
