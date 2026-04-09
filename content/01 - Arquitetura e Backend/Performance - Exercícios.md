# Performance - Bateria de Exercícios

Foque na resiliência e na escalabilidade do seu código .NET.

---

## 🎮 Prática: Side Quest (CancellationToken)
No seu projeto `.NET`, adicione o parâmetro `CancellationToken ct` em um método de Controller e passe ele para dentro do `ToListAsync(ct)`.
1. Use `await Task.Delay(5000, ct);` para simular uma query lenta.
2. Dispare a requisição via navegador ou Postman.
3. Cancele a requisição no meio do carregamento.
4. Verifique nos logs se o .NET disparou uma exceção de cancelamento (ou se o processo parou imediatamente).

---

## 📜 XP Check (10 Questões de Checklist)

1. **(Performance)** O que acontece com a thread original da requisição HTTP quando usamos `.ConfigureAwait(false)` em um método assíncrono?
2. **(Segurança)** Como o uso de Parâmetros Nomeados (ex: `@id`) evita um ataque de SQL Injection?
3. **(Recursos)** Um usuário fechou a aba do navegador antes do relatório carregar. Qual objeto é responsável por avisar ao banco que ele pode parar de trabalhar?
4. **(Concorrência)** O `.ConfigureAwait(false)` é recomendado em aplicações Desktop (Windows Forms/WPF) que mexem na UI? Por quê?
5. **(Banco de Dados)** No Entity Framework, por que passar o `CancellationToken` para o `SaveChangesAsync()` é uma boa prática?
6. **(RPG)** Se um jogador dispara uma flecha e o servidor cai, a flecha não deve atingir o alvo. Como você usaria o conceito de atomicidade nesse cenário?
7. **(C#)** Qual a diferença entre `Task.Delay(1000)` e `Thread.Sleep(1000)` em um ambiente de alta performance?
8. **(Performance)** Por que a concatenação de strings em queries SQL (`"SELECT * FROM Users WHERE Name = " + name`) é perigosa?
9. **(Deadlock)** Como o uso correto do `Async/Await` e `ConfigureAwait` ajuda a evitar travamentos de servidor (Deadlocks)?
10. **(Checklist)** Em um Code Review, você vê um código que faz 500 chamadas ao banco dentro de um `foreach`. Qual termo técnico você usaria para descrever esse problema de performance? (Dica: N+1).

---

## 💡 Precisa de Ajuda?
As respostas explicadas estão no arquivo:
[[Gabarito dos Exercícios]]



