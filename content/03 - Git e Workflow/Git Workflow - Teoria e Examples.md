# Domínio do Git no Dia a Dia (Deep Dive)

Junior, o Git não é apenas uma ferramenta de "salvamento". Ele é um **Grafo de Estados**. Se você entender como os nós desse grafo se conectam, você nunca mais terá medo de um `merge conflict` ou de um `detached HEAD`.

---

## 🧠 1. Anatomia do Git: O que é um Commit?
Diferente de outras ferramentas, o Git não guarda "mudanças de linha", ele guarda **Snapshots** (fotos) de todos os arquivos do seu projeto.
- **Blob:** O conteúdo de um arquivo.
- **Tree:** Uma pasta (que contém Blobs ou outras Trees).
- **Commit:** Uma Tree + Mensagem + Autor + Link para o Commit Anterior (Pai).

### **Transcrição Técnica: A Área de Stage**
> "O Git possui três áreas principais: o **Diretório de Trabalho** (onde você digita), a **Área de Preparação (Index/Stage)** e o **Repositório (.git)**. O comando `git add` é o que move os dados do seu diretório para o Index, preparando o Snapshot para o commit."
> *Ref: Documentação Oficial Git*

---

## 🚀 2. Estratégias de Ramificação (Branching)
O FinanceiraEstude precisa de uma estratégia para que você e outros devs não se batam.
- **Trunk-Based Development:** Todos trabalham na `main`. Branches duram poucas horas. Ideal para CI/CD agressivo.
- **GitHub Flow:** Branches de feature curtas. Quando termina, abre um Pull Request (PR). É o que vamos usar no FinanceiraEstude.
- **⚠️ Perigo: Long-lived branches.** Branches que duram 2 semanas. Quando você tentar mesclar, o mundo terá mudado e você terá 200 conflitos. **Faça commits e merges pequenos e frequentes.**

---

## 🏗️ 8 Exemplos Práticos de Comando e Poder

### 🗡️ Exemplo 1: O Botão de Pânico (Hard Reset)
Se você estragou tudo localmente e quer voltar ao estado do servidor:
```bash
git fetch origin
git reset --hard origin/main
```

### 🗡️ Exemplo 2: Recuperando o "Impossível" (Reflog)
Deletou uma branch sem querer? O Git guarda o histórico de onde o seu `HEAD` apontou nos últimos 30 dias.
```bash
git reflog
# Ache o hash do commit e faça:
git checkout -b branch-recuperada [hash]
```

### 🗡️ Exemplo 3: Conventional Commits
Não escreva "ajuste". Escreva:
`feat: adiciona validacao de valor negativo no aporte`
`fix: corrige erro de arredondamento no calculo de juros`

### 🗡️ Exemplo 4: Rebase Interativo (Squash)
Una 10 commits de "teste" em um só antes de subir o PR.
```bash
git rebase -i HEAD~10
# No editor, mude 'pick' para 'squash' nos commits de baixo.
```

### 🗡️ Exemplo 5: Cherry-pick (A Cereja do Bolo)
Você corrigiu um bug crítico em uma branch de teste e quer levar APENAS esse commit para a `main`.
```bash
git checkout main
git cherry-pick [hash-do-commit]
```

### 🗡️ Exemplo 6: Git Stash (O Porta-Luvas)
Precisa trocar de branch rápido mas não quer cometer código incompleto?
```bash
git stash # Guarda tudo
git checkout outra-branch
# Depois volta e faz:
git stash pop # Traz de volta
```

### 🗡️ Exemplo 7: Amend (Corrigindo o Último Commit)
Esqueceu um arquivo ou errou a mensagem do commit que acabou de fazer?
```bash
git add .
git commit --amend --no-edit
```

### 🗡️ Exemplo 8: Blame e Log (Arqueologia)
Quem mudou essa linha e por quê?
`git blame [arquivo]`
`git log -p [arquivo]` (Vê o histórico de mudanças dentro do arquivo).

---

## 👨‍💻 Visão Sênior: Commits são Documentação
Junior, um bom desenvolvedor gasta tempo escrevendo mensagens de commit claras. Daqui a 6 meses, quando você encontrar um bug, o commit será a sua única pista de **por que** você tomou aquela decisão bizarra às 3h da manhã. O código diz **O QUE**, o commit diz **POR QUÊ**.

---

## 💡 Próximos Passos
Domine o seu histórico de código:
[[Git Workflow - Exercícios]]
