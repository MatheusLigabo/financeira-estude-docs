# DDD - Bateria de Exercícios

Este arquivo é focado em testar seu conhecimento prático e teórico sobre Domain-Driven Design. Tente resolver sem olhar o gabarito!

---

## 🎮 Prática: Side Quest
Abra seu projeto pessoal (**FinanceiraEstude**) e identifique uma classe que hoje seja apenas uma "sacola de dados" (apenas properties com `get; set;`).
1. Altere os setters para `private set`.
2. Crie um método com um nome que faça sentido para o negócio (ex: `AprovarPedido()`, `DebitarEstoque()`).
3. Adicione uma validação dentro desse método.

---

## 📜 XP Check (10 Questões de Fixação)

1. **(RPG)** O Herói tenta equipar uma "Armadura Lendária", mas ele não tem o nível necessário. Segundo o DDD, onde deve ficar a validação `SeNivelValido()`?
2. **(Logística)** Um caminhão não pode exceder 10 toneladas. Se eu criar um método `Caminhao.AdicionarCarga(peso)`, estou seguindo qual princípio do DDD?
3. **(Conceito)** O que é "Linguagem Onipresente" (Ubiquitous Language) em uma reunião com o cliente?
4. **(Arquitetura)** Se eu trocar o banco SQL pelo MongoDB, qual camada do sistema **não** deve sofrer nenhuma alteração de código?
5. **(DDD)** Por que o "Modelo Anêmico" é considerado um anti-padrão?
6. **(RPG)** Um `NPC` e um `Inimigo` podem ter propriedades parecidas. Devo usar a mesma classe para os dois só porque os dados são iguais?
7. **(Pragmatismo)** Se o prazo está apertado e a tela é apenas um relatório de leitura, o uso de CQRS completo é obrigatório?
8. **(Encapsulamento)** O que significa o termo "Tell, Don't Ask"?
9. **(Infra)** Por que as Interfaces (Contratos) ficam no Domínio e não na camada de Infraestrutura?
10. **(Design)** No DDD, quem deve ser o "dono" da regra matemática de um cálculo de juros de uma parcela? A Controller ou a Entidade `Parcela`?

---

## 💡 Precisa de Ajuda?
As respostas explicadas estão no arquivo:
[[Gabarito dos Exercícios]]




