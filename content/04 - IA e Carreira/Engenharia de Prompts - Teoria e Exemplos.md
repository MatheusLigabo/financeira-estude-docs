# Engenharia de Prompts e IA (Deep Dive)

Junior, a IA não é mágica, é **Previsão Estatística de Tokens**. Se você entender como o modelo "pensa", você consegue transformá-la no seu melhor Pair Programmer para o FinanceiraEstude.

---

## 🧠 1. Como a IA Funciona: Tokens e Janelas de Contexto
A IA não lê "palavras", ela lê **Tokens** (fragmentos de palavras).
- **Janela de Contexto (Context Window):** É a memória de curto prazo da IA. Se você colar 10 arquivos gigantes, ela pode começar a esquecer as regras lá de cima. 
- **⚠️ Perigo: Alucinação.** Quando a IA não tem a resposta, ela inventa uma que soa convincente. O seu papel como sênior em treinamento é **Validar Tudo**.

### **Transcrição Técnica: LLMs e Predição**
> "Modelos de Linguagem (LLMs) são treinados para prever o próximo token em uma sequência. Eles não possuem um 'entendimento' real do mundo, mas sim um mapeamento probabilístico ultra sofisticado de como os conceitos se relacionam."
> *Ref: Documentação OpenAI/Anthropic*

---

## 🚀 2. Técnicas de Prompting Avançadas
Para que a IA gere código de nível sênior, você precisa de técnica:
- **Zero-Shot:** Pedir algo do nada. (Risco médio de erro).
- **Few-Shot:** Dar 2 ou 3 exemplos do seu padrão de código antes de pedir a tarefa final. (Alta precisão).
- **Chain of Thought (CoT):** Pedir para a IA "explicar passo a passo antes de escrever o código". Isso força o modelo a seguir um raciocínio lógico.

---

## 🏗️ 8 Exemplos Práticos de IA no FinanceiraEstude

### 🗡️ Exemplo 1: Refatoração com Contexto
"Atue como um Sênior em .NET. Refatore este código seguindo os padrões do meu arquivo `Aporte.cs` que acabei de te enviar."

### 🗡️ Exemplo 2: O Prompt "Borracha" (Limpar Código)
"Remova todos os comentários desnecessários, simplifique os ifs e transforme este loop em um comando LINQ elegante."

### 🗡️ Exemplo 3: Geração de Testes com Edge Cases
"Gere testes unitários xUnit para este Handler. Não esqueça dos cenários de erro (Valor Negativo, Banco Fora, Usuário não encontrado)."

### 🗡️ Exemplo 4: Engenharia Reversa (Network Tab)
Cole um JSON da aba Network do seu navegador e peça: "Mapeie este JSON para uma estrutura C# record seguindo os nomes em CamelCase."

### 🗡️ Exemplo 5: O "Explainer" de Documentação
"Explique como o RabbitMQ gerencia o Ack (Acknowledgement) de mensagens como se eu fosse um Junior, e me dê um exemplo em C#."

### 🗡️ Exemplo 6: Setup de Boilerplate
"Baseado na Clean Architecture do FinanceiraEstude, gere a estrutura básica (Controller, DTO, UseCase, Repository) para a nova funcionalidade de 'Saques'."

### 🗡️ Exemplo 7: Caça aos Bugs
"Este código está dando `NullReferenceException`. Analise a lógica e aponte onde o nulo pode estar nascendo e sugira uma Guard Clause."

### 🗡️ Exemplo 8: Otimizador de SQL
"Analise esta query SQL. Ela está fazendo Scan na tabela inteira. Sugira como criar um índice ou refatorar o Join para usar o Primary Key."

---

## 👨‍💻 Visão Sênior: A IA é seu Estagiário, não seu Arquiteto
Junior, se você pedir para a IA "fazer o sistema para mim", o resultado será um desastre genérico. Use a IA para **tarefas modulares e repetitivas** (gerar testes, refatorar um método, explicar uma Regex). O desenho da arquitetura e a segurança final do FinanceiraEstude são **sua responsabilidade**.

---

## 💡 Próximos Passos
Domine o seu novo braço direito:
[[Engenharia de Prompts - Exercícios]]


