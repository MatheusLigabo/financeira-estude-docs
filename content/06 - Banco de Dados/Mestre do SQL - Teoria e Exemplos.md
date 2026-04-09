# Módulo 06: Mestre do SQL (Do Zero à Alta Performance)

Junior, no FinanceiraEstude, se o banco de dados cair, o sistema morre. O SQL é a linguagem que garante a imortalidade e a segurança dos dados. Se você não souber o que é uma **Transação**, você vai corromper o patrimônio dos usuários.

## 🧠 1. Modelagem: As Formas Normais
- **1ª Forma Normal (1FN):** Sem grupos repetidos. Cada célula tem um único valor (ex: não coloque "Telefone1, Telefone2" na mesma linha).
- **2ª Forma Normal (2FN):** Tudo deve depender da chave primária (ex: se o ClienteID está na tabela Aportes, o "Nome do Cliente" não deve estar, pois depende de outra tabela).
- **3ª Forma Normal (3FN):** Sem dependências transitivas. Se mudar um dado, você não deve ter que atualizar em 10 lugares diferentes.

## 🔗 2. Joins Avançados e o Problema N+1
Muitos juniores acham que o banco de dados é uma planilha do Excel. Não é.
- **INNER JOIN:** É uma interseção. Só traz se houver correlação.
- **LEFT JOIN:** É uma junção de inclusão. Útil para: "Me dê todos os clientes, mesmo aqueles que ainda não fizeram nenhum aporte".
- **O PROBLEMA N+1:** Se você fizer um `SELECT * FROM Aportes` e depois um loop no C# para buscar o Cliente de cada aporte, seu sistema vai travar. **FAÇA TUDO EM UMA ÚNICA QUERY COM JOIN.**

## 🛡️ 3. Transações (ACID) - O Cinto de Segurança
Imagine uma transferência financeira. Você tira 100 reais de uma conta e, no meio do processo, o servidor cai. O dinheiro sumiu?
**A Solução: Transações (BEGIN, COMMIT, ROLLBACK).**
Ou tudo acontece com perfeição, ou nada acontece e o banco volta ao estado anterior. Isso é **Atomicidade**.

---

## 🏗️ 8 Exemplos Práticos de Poder SQL

### 🗡️ Exemplo 1: O Join de Aportes
```sql
SELECT c.Nome, a.Valor, a.Data 
FROM Aportes a 
JOIN Clientes c ON a.ClienteId = c.Id
WHERE a.Valor > 5000;
```

### 🗡️ Exemplo 2: Agregação por Mês
Como o FinanceiraEstude vai mostrar o gráfico mensal?
```sql
SELECT FORMAT(Data, 'yyyy-MM') as Mes, SUM(Valor) as Total
FROM Aportes
GROUP BY FORMAT(Data, 'yyyy-MM');
```

### 🗡️ Exemplo 3: Paginação de Alta Performance
Nunca use `SELECT *`. Traga apenas o necessário com `OFFSET/FETCH`.
```sql
SELECT Id, Valor, Data 
FROM Aportes 
ORDER BY Data DESC 
OFFSET 20 ROWS FETCH NEXT 10 ROWS ONLY;
```

### 🗡️ Exemplo 4: Subqueries e Existência
Verificar quais clientes nunca fizeram aportes:
```sql
SELECT Nome FROM Clientes 
WHERE NOT EXISTS (SELECT 1 FROM Aportes WHERE ClienteId = Clientes.Id);
```

### 🗡️ Exemplo 5: Índices Compostos
Se você sempre busca por `ClienteId` + `Data`, crie um índice que cubra as duas colunas juntas. A busca será instantânea.
```sql
CREATE INDEX IX_Cliente_Data ON Aportes(ClienteId, Data);
```

### 🗡️ Exemplo 6: SQL Injection (O Escudo)
No C#, use Dapper ou Entity Framework com parâmetros. Nunca faça isto:
`string sql = "SELECT * FROM Users WHERE Nome = '" + input + "'";` // BURACO DE SEGURANÇA!

### 🗡️ Exemplo 7: CTE (Common Table Expressions)
Para queries complexas e legíveis, use o `WITH`:
```sql
WITH UltimosAportes AS (
    SELECT ClienteId, MAX(Data) as UltimaData FROM Aportes GROUP BY ClienteId
)
SELECT c.Nome, ua.UltimaData FROM Clientes c JOIN UltimosAportes ua ON c.Id = ua.ClienteId;
```

### 🗡️ Exemplo 8: UPSERT (Update or Insert)
Tentar atualizar um registro e, se não existir, inserir:
```sql
IF EXISTS (SELECT 1 FROM Config WHERE Chave = 'Moeda')
    UPDATE Config SET Valor = 'BRL' WHERE Chave = 'Moeda'
ELSE
    INSERT INTO Config (Chave, Valor) VALUES ('Moeda', 'BRL');
```

---

## 👨‍💻 Visão Sênior: O custo de uma rede congestionada
Junior, o banco de dados pode estar em um servidor e sua API em outro. Se você der um `SELECT *` em uma tabela de 100 colunas só para usar 2, você está entupindo a rede com dados inúteis. Peça apenas o necessário. No FinanceiraEstude, escalabilidade começa na consulta SQL eficiente.

*Documentação Essencial:* [Guia de SQL da Microsoft (T-SQL)](https://learn.microsoft.com/pt-br/sql/t-sql/language-reference)

---

## 💡 Próximos Passos
🔗 **[Abrir Laboratório de SQL no VS Code](vscode://file/C:/Users/mtsli/OneDrive/%C3%81rea%20de%20Trabalho/Futuro/FinanceiraEstude/FinanceiraEstude/Exercises/Database/Pratica_SQL.cs)**



