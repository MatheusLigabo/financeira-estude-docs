# 🏆 Gabarito dos Exercícios e Desafios

Este arquivo contém as respostas e explicações para as questões de fixação presentes em cada módulo do seu Dashboard. Use-o para validar seu conhecimento após tentar responder por conta própria!

---

## 🗡️ 1. Domain-Driven Design (DDD)
1. **Onde fica a validação?** Na **Entidade** `Armadura` ou no **Objeto de Valor** `RequisitoNivel`. O Domínio deve se auto-validar.
2. **Qual princípio?** **Encapsulamento** (ou "Tell, Don't Ask"). Você não altera o peso de fora, você "pede" para o caminhão adicionar carga e ele decide se pode.
3. **Linguagem Onipresente:** É usar os mesmos termos que o cliente usa (ex: "Aferição", "Glosa", "Sinistro") dentro do código (classes, métodos, variáveis).
4. **Camada imune:** O **Domínio** (Domain) e a **Aplicação** (Application). Apenas a Infraestrutura muda.
5. **Modelo Anêmico:** Porque ele transforma objetos em meras sacolas de dados, espalhando a lógica de negócio por todo o sistema (Controllers, Services), dificultando a manutenção.
6. **NPC vs Inimigo:** Não. Se as regras de negócio forem diferentes (ex: Inimigo ataca, NPC negocia), eles devem ser classes separadas mesmo que tenham propriedades parecidas.
7. **Pragmatismo:** Não. Se for algo simples e de leitura, um acesso direto (Dapper/SQL) é mais eficiente e rápido.
8. **Tell, Don't Ask:** "Diga o que fazer, não pergunte dados para tomar a decisão fora da classe".
9. **Interfaces no Domínio:** Para inverter a dependência. O Domínio define *o que* precisa (contrato), e a Infraestrutura decide *como* fazer (implementação).
10. **Dono da regra:** A **Entidade** `Parcela`.

---

## 🚀 2. Performance Backend
1. **ConfigureAwait(false):** Ela avisa que a thread de continuação não precisa ser a mesma que iniciou a tarefa, liberando o contexto de sincronização.
2. **SQL Injection:** Ele trata o valor como um dado puro e não como parte do comando SQL, impedindo que comandos maliciosos sejam executados.
3. **Objeto de cancelamento:** O `CancellationToken`.
4. **Desktop Apps:** Geralmente **não** é recomendado na thread de UI, pois a UI precisa de sincronização para atualizar elementos visuais. No Backend (Web API) é altamente recomendado.
5. **SaveChangesAsync:** Se o usuário cancelar a requisição enquanto o banco está salvando, o processo é interrompido, economizando recursos.
6. **Atomicidade:** Ou a flecha atinge e causa dano (tudo), ou nada acontece (nada). Não pode causar dano sem a flecha existir.
7. **Delay vs Sleep:** `Task.Delay` é assíncrono (não trava a thread), `Thread.Sleep` é síncrono (trava a thread inteira).
8. **Concatenação:** Porque permite que um usuário envie algo como `'1; DROP TABLE Users'` e o banco execute.
9. **Deadlocks:** Ao liberar a thread original, você evita que duas threads fiquem esperando uma pela outra infinitamente.
10. **N+1:** Fazer uma query principal e depois uma query para cada item do resultado em vez de usar um `Join` ou `Include`.

---

## 🌐 3. Gerenciamento de Estado (Front)
1. **Benefício URL:** Permite compartilhar o link com o estado exato da tela (filtros, paginação) e sobrevive ao F5.
2. **Lifting State Up:** Mover o estado para o componente pai comum mais próximo para que vários filhos possam acessá-lo.
3. **Sobrevivência:** `Local Storage`.
4. **Performance:** O acesso ao storage é síncrono e lento; além disso, há um limite de tamanho (geralmente 5MB).
5. **Segurança:** Sim, ele pode. O Backend **sempre** deve validar as permissões no JWT/Cookie a cada requisição, nunca confiar no Front.
6. **Wizard Personagem:** `Session Storage` ou `URL`.
7. **Single Source of Truth:** Ter apenas um lugar onde o dado "mestre" reside, evitando duplicidade e inconsistência.
8. **Hook de efeito:** `useEffect`.
9. **Params vs Query:** `Route Params` para recursos obrigatórios (`/user/10`); `Query Params` para filtros/opcionais (`/users?status=ativo`).
10. **Estado Global:** Deve ser evitado para dados que apenas 2 ou 3 componentes próximos usam. Use `props` ou `composition` primeiro.

---

## 🐙 4. Domínio do Git
1. **Botão de Pânico:** `git reset --hard origin/nome-da-branch`.
2. **Pull na Main:** Para garantir que você tem as últimas atualizações dos outros devs e resolver conflitos antes de enviar seu código.
3. **git add .:** Coloca todos os arquivos alterados na "Staging Area" (preparação para o commit).
4. **Soft Reset:** `git reset --soft HEAD~1`.
5. **Marcas de conflito:** `HEAD` é o que está na sua branch atual; `feature-x` é o que vem da branch que você está tentando mesclar.
6. **Fetch vs Pull:** `Fetch` apenas baixa as novidades sem mexer no seu código. `Pull` faz o `fetch` e já tenta mesclar (`merge`) no seu código.
7. **Histórico:** `git log`.
8. **Guardar código:** `git stash`.
9. **.gitignore:** Para dizer ao Git quais arquivos/pastas ele deve ignorar (ex: `node_modules`, `bin/`, `.env`).
10. **Code Review:** É a revisão do seu PR por outro dev. O Git permite ver exatamente o que mudou (diff) facilitando a crítica construtiva.

---

## 🤖 5. Engenharia de Prompts
1. **Context Window:** É a quantidade de informação (memória) que a IA consegue processar de uma vez em uma conversa.
2. **Referenciar arquivo:** Dá um exemplo real do seu estilo de código, evitando que a IA gere algo fora do padrão da sua empresa.
3. **Prompt Estruturado:** Contém Contexto, Objetivo, Instruções Negativas (o que não fazer) e Formato de Saída.
4. **IA vs Lógica:** Não substitui. Você precisa da lógica para validar se o que a IA gerou está certo e para arquitetar o sistema.
5. **Segurança:** Seus dados podem ser usados para treinar modelos futuros ou serem acessados por funcionários da empresa de IA. Nunca cole dados sensíveis.
6. **Alucinação:** Quando a IA inventa uma biblioteca ou função que não existe. Valide tentando compilar ou pesquisando na documentação oficial.
7. **Testes Unitários:** Você pode colar sua classe e pedir: "Gere testes unitários usando xUnit cobrindo os caminhos felizes e de erro".
8. **Network Tab:** Permite ver o JSON real que o sistema antigo usa, fornecendo a "verdade" técnica para a IA mapear.
9. **Zero vs Few-Shot:** `Zero-shot` é pedir sem exemplos. `Few-shot` é dar 2 ou 3 exemplos antes do pedido final.
10. **Simular Entrevista:** "Atue como um Mentor e me faça 5 perguntas difíceis sobre .NET Internals. Avalie minhas respostas no final."

---

## 📅 6. Sistema Learn vs Earn
1. **Diferença:** `Learn` foca em fundamentos e perfeccionismo (estudo). `Earn` foca em valor, prazos e regras de negócio reais (trabalho).
2. **Trabalho não é escola:** Porque no trabalho o foco é a entrega rápida. Se você tentar aprender a base lá, vai se frustrar com a pressão.
3. **Blindagem de Tempo:** Reservar um horário sagrado onde nada (celular, reuniões, TV) atrapalha seu foco.
4. **Legado como material:** Analisar por que aquele código é ruim, como ele poderia ser melhor e quais padrões ele quebra.
5. **Literatura:** Melhora a interpretação de texto, ajudando a entender requisitos complexos e a nomear melhor suas variáveis e métodos.
6. **Tecnologia nova:** Aprenda o "mínimo viável" para entregar no trabalho, mas aprofunde a base no seu tempo de `Learn`.
7. **Aprender tudo:** Gera sobrecarga cognitiva e você acaba não aprendendo nada profundamente. Foco é dizer "não" para outras tecnologias.
8. **Pomodoro:** Evita a fadiga mental e treina seu cérebro para focar intensamente por períodos curtos.
9. **Falha de rotina:** Não se culpe. Simplesmente volte no dia seguinte como se nada tivesse acontecido. O segredo é a consistência, não a perfeição.
10. **Qual o mais perfeito?** O projeto **Learn**. É lá que você treina para ser um mestre; no `Earn`, você é um executor de elite.

---

## 🏗️ 0. C# Fundamentos (Gabarito)
1. **Valor vs Referência:** `int`, `decimal`, `Guid` são de valor (copia o dado). `string`, `class` são de referência (copia o endereço na memória).
2. **Double vs Decimal:** Use `decimal` para dinheiro. `double` arredonda centavos (erro de precisão binária).
3. **LINQ:** `.Where()` filtra, `.Select()` projeta, `.Sum()` soma.
4. **Dictionary:** A busca em um `Dictionary<TKey, TValue>` é imediata (O(1)). Em uma `List<T>`, o C# precisa ler todos os itens até achar o seu (O(n)).
5. **Debug:** F10 passa a linha, F11 entra no método. Use o "Watch" para vigiar variáveis.

---

## 🛢️ 6. Mestre do SQL (Gabarito)
1. **Join Correto:** `SELECT c.Nome, a.Valor FROM Aportes a INNER JOIN Clientes c ON a.ClienteId = c.Id`.
2. **N+1:** Fazer uma query e depois um loop de queries individuais. O Join resolve isso trazendo tudo de uma vez.
3. **Delete sem Where:** O maior erro de um dev. Apaga a tabela inteira.
4. **SQL Injection:** Injectar comandos maliciosos via inputs de texto. Resolvido com `Parameters` (ex: `@id`).
5. **Indice:** Aumenta a velocidade de leitura, mas diminui um pouco a de escrita (pois o índice precisa ser atualizado no `INSERT`).

---

## 💣 7. Simulador de Caos (Correção de Bugs)

Abaixo estão as soluções e os **Caminhos de Decisão** para os 50 erros do FinanceiraEstude.

### 🏗️ Bloco 1: O Domínio Corrompido (`Aporte.cs`)
*   **A Solução (Domínio Rico):**
    *   Remover `set` público (usar `private set`).
    *   Remover construtor vazio (obrigatoriedade de dados válidos).
    *   Validar valor `<= 0` no construtor.
    *   Gerar o `Id` no construtor (autonomia da entidade).
    *   Implementar Enum de `Status`.
*   **Caminhos Possíveis:**
    1.  **Caminho Purista (DDD):** A entidade lança uma `DomainException`. O `Id` é um `Guid` ou um Objeto de Valor. (Este é o caminho ideal).
    2.  **Caminho Pragmático (CRUD):** As propriedades ficam públicas para o EF Core, mas as validações ficam em um `Validator` (FluentValidation). *Pode funcionar, mas fere o encapsulamento.*

### 🎼 Bloco 2: O Maestro Desafinado (`RealizarAporteUseCase.cs`)
*   **A Solução (Application Layer):**
    *   Injetar `IAporteRepository` no construtor (Inversão de Dependência).
    *   Usar `async/await` em toda a cadeia.
    *   Remover validações de negócio (deixar a Entidade validar).
    *   Remover `Console.WriteLine` (usar `ILogger`).
*   **Caminhos Possíveis:**
    1.  **Caminho MediatR:** O Use Case vira um `Handler` (CQRS). Isolamento total.
    2.  **Caminho Service:** Criar uma interface `IAporteService`. *Mais simples, mas tende a acumular lógica desnecessária.*

### 🛎️ Bloco 3: O Balcão de Vidro (`AportesController.cs`)
*   **A Solução (API Layer):**
    *   Usar DTOs (`AporteRequest`) em vez de tipos primitivos.
    *   Repassar o `CancellationToken` para o Use Case.
    *   Remover o `new` do Use Case (usar Injeção de Dependência).
    *   Mapear exceções globais em um Middleware.
*   **Caminhos Possíveis:**
    1.  **Minimal APIs:** Mais performático para serviços pequenos.
    2.  **Controllers Tradicionais:** Melhor para sistemas complexos com muitos filtros.

### 🦾 Bloco 4: A Infraestrutura de Papel (`AporteRepository.cs`)
*   **A Solução (Infrastructure Layer):**
    *   Usar `Dapper` ou `EF Core` com parâmetros nomeados (evitar `@valor + x`).
    *   Usar `ConfigureAwait(false)`.
    *   Gerenciar conexão via `IDbConnection` injetada pelo .NET (Pool).
*   **Caminhos Possíveis:**
    1.  **Repository Pattern Puro:** Esconde totalmente o ORM.
    2.  **Unit of Work:** Garante que várias operações no banco sejam uma transação única.

### 🤖 Bloco 5: O Worker Zumbi (`Worker.cs`)
*   **A Solução (Worker Service):**
    *   Usar `await Task.Delay` com o `stoppingToken`.
    *   Implementar `BasicAck` para confirmar que a mensagem foi processada no RabbitMQ.
    *   Usar `IServiceScopeFactory` para criar escopos Scoped dentro do Background Service (Singleton).
*   **Caminhos Possíveis:**
    1.  **MassTransit:** Abstração de alto nível para RabbitMQ (mais seguro).
    2.  **RabbitMQ Client Puro:** Mais controle, mas exige que você trate as falhas manualmente.

---
**Dica Final:** Se o que você fez resolve o erro (ex: transformou o `set` em `private set`), você está no caminho certo! O importante é entender **por que** a propriedade pública é perigosa.



