# Domínio do Git no Dia a Dia

O Git não é apenas uma ferramenta de backup de código; é uma ferramenta de **colaboração e documentação histórica**. Um repositório bem organizado conta a história da evolução do software.

## 🧠 Fluxos de Trabalho (Workflows)

### 1. Trunk-Based Development
É o fluxo preferido por empresas de alta performance (como Google e Netflix). Os Deves fazem commits pequenos e frequentes diretamente na `main` (ou branches de vida curtíssima).
- **Vantagem:** Evita "Hell Merge" (conflitos gigantes) no final da feature.

### 2. Git Flow
Usa branches separadas para `develop`, `feature`, `release` e `hotfix`. 
- **Vantagem:** Controle rigoroso do que entra em produção. Ideal para sistemas legados ou com ciclos de release lentos.

---

## 🏗️ 4 Exemplos de Poder do Git

### 🚑 Exemplo 1: Hotfix de Emergência
**Cenário:** Um bug crítico apareceu em produção, mas sua branch de feature está pela metade e não pode subir.
**Solução:** 
1. `git stash` (guarda seu trabalho incompleto).
2. `git checkout main` -> `git pull`.
3. Crie a branch `hotfix/erro-banco`.
4. Corrija, suba o PR.
5. `git checkout sua-feature` -> `git stash pop` (volta ao trabalho).

### 🧹 Exemplo 2: Rebase Interativo (Squash)
**Cenário:** Você fez 10 commits com mensagens como "ajuste", "fix", "teste". 
**Solução:** Use o rebase interativo para unir todos em um único commit limpo antes de abrir o PR.
`git rebase -i HEAD~10`

### ⚔️ Exemplo 3: Resolução de Conflito Complexo
**Cenário:** Duas pessoas alteraram a mesma lógica de cálculo.
**Dica Sênior:** Nunca resolva conflitos no Github/Gitlab. Sempre faça o `merge main` na sua branch localmente e use uma ferramenta de diff (como o VS Code) para comparar linha a linha.

### 🕰️ Exemplo 4: O Milagre do `git reflog`
**Cenário:** Você deletou uma branch importante por engano ou fez um `reset --hard` e perdeu tudo.
**Solução:** O `git reflog` mostra o histórico de **tudo** que você fez localmente, permitindo recuperar commits que "sumiram".

---

## 👨‍💻 Visão Sênior: Commits que Contam uma História

**A "Preguiça do Commit":**
Vejo muitos Deves enviando PRs com 50 arquivos alterados e uma mensagem "ajustes gerais". Isso é um pesadelo para quem revisa.

**O Conselho do Mentor:**
1. **Commits Atômicos:** Um commit deve fazer apenas UMA coisa. Se você corrigiu um bug e formatou o arquivo, faça dois commits separados.
2. **Mensagens Semânticas:** Use padrões como *Conventional Commits* (`feat:`, `fix:`, `refactor:`).
3. **Pequeno e Frequente:** É muito melhor resolver 5 conflitos pequenos por dia do que 1 conflito gigante na sexta-feira às 18h. O Git recompensa quem é organizado.

---

## 💡 Próximos Passos
Teste seu domínio de terminal no arquivo:
[[Git Workflow - Exercícios]]



