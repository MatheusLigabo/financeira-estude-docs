# Gerenciamento de Estado - Bateria de Exercícios

Foque na fluidez da experiência do usuário e na organização do seu código React.

---

## 🎮 Prática: Side Quest (URL Params)
No seu projeto React, crie uma lista simples de itens (ex: `['Espada', 'Escudo', 'Poção']`).
1. Use o hook `useSearchParams` do `react-router-dom`.
2. Crie um campo de input que, ao digitar, atualiza a URL (ex: `?busca=espada`).
3. Filtre a lista baseado no que está na URL.
4. Tente dar Refresh (F5) na página e veja se o filtro continua aplicado.

---

## 📜 XP Check (10 Questões de Arquitetura Front)

1. **(Frontend)** Qual o maior benefício de manter o estado de filtros de uma tabela na URL (Query Params)?
2. **(React)** Se um componente pai passa uma função de alteração de estado para o filho, como chamamos esse padrão? (Dica: "Lifting State Up").
3. **(Browser)** Qual o armazenamento que sobrevive mesmo quando você fecha o navegador completamente?
4. **(Performance)** Por que não devemos guardar uma lista de 5.000 itens no `Local Storage`?
5. **(Segurança)** Se eu guardo um dado de permissão (`isAdmin: true`) no `Session Storage`, o usuário pode alterar isso manualmente no Console do Chrome? O que o Backend deve fazer?
6. **(UX)** Em um formulário de "Criação de Personagem" com 5 passos (Wizard), qual o melhor armazenamento para que o progresso não se perca se ele mudar de aba, mas limpe quando ele fechar o navegador?
7. **(SPA)** O que significa o termo "Single Source of Truth" (Fonte Única de Verdade) em gerenciamento de estado?
8. **(React)** Qual hook é usado para disparar um efeito colateral quando uma variável de estado muda?
9. **(URL)** Qual a diferença entre `Route Params` (ex: `/perfil/dev_user`) e `Query Params` (ex: `/perfil?user=dev_user`)? Quando usar cada um?
10. **(Estado)** O que é o "Estado Global" (como Redux ou Context API) e em que cenário ele deve ser evitado? (Dica: Prop drilling simples).

---

## 💡 Precisa de Ajuda?
As respostas explicadas estão no arquivo:
[[Gabarito dos Exercícios]]


