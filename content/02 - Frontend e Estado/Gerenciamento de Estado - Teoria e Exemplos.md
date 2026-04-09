# Estratégias de Gerenciamento de Estado no Front (Deep Dive)

Junior, o Front-end moderno não é apenas "tela". É um **Sistema Distribuído** que precisa sincronizar dados com o servidor. Se você não gerenciar bem o estado, sua aplicação React vai virar uma "bagunça" de re-renderizações inúteis e bugs de UI.

---

## 🧠 1. Anatomia do Estado e Ciclo de Vida do React
O React é declarativo. Você define o estado, e o React decide como desenhar na tela.
- **O Re-render:** Toda vez que um estado (`useState`) muda, o componente **inteiro** e seus filhos são recalculados. 
- **⚠️ Perigo: Loop de Renderização.** Se você alterar o estado dentro do corpo do componente sem um `useEffect`, você cria um loop infinito que trava o navegador do usuário.

### **Transcrição Técnica: Virtual DOM e Reconciliação**
> "O React cria uma cópia leve do DOM real na memória. Quando o estado muda, ele compara o novo Virtual DOM com o antigo e aplica **apenas** as mudanças necessárias no DOM real. Isso é o que torna o React rápido."
> *Ref: Documentação Oficial React*

---

## 🚀 2. Server State vs. Client State
Junior, pare de usar `useEffect` para buscar dados da API. Isso é padrão de 2018.
- **Client State:** Dados puramente locais (modal aberto, input digitado).
- **Server State:** Dados que vêm do banco (lista de aportes). Use **React Query (TanStack Query)**.
  - Ele cuida do Cache.
  - Ele cuida do Loading e Error automaticamente.
  - Ele evita "bater" no banco 10 vezes se você clicar no botão de novo.

---

## 🌐 3. Sincronização via URL (A Fonte da Verdade)
Filtros de busca, paginação e abas selecionadas **devem** estar na URL.
*Por que?* Se o usuário der F5 ou mandar o link para o suporte, a tela abre exatamente onde ele parou. Use o `useSearchParams`.

---

## 🏗️ 8 Exemplos Práticos no Frontend

### 🗡️ Exemplo 1: URL Params para Filtros
```jsx
const [searchParams, setSearchParams] = useSearchParams();
const categoria = searchParams.get('categoria') || 'todos';

// O filtro "vive" na URL, não no estado local!
```

### 🗡️ Exemplo 2: React Query para Buscar Aportes
```jsx
const { data, isLoading } = useQuery(['aportes'], fetchAportes);
// Sem useEffect, sem controle de loading manual. Código limpo.
```

### 🗡️ Exemplo 3: LocalStorage para Preferências
```jsx
// Use para coisas que NÃO mudam com frequência, como Tema (Dark/Light).
localStorage.setItem('tema', 'dark');
```

### 🗡️ Exemplo 4: Lifting State Up (Subindo o Estado)
Se dois componentes (ex: Header e Sidebar) precisam do nome do usuário, o estado deve morar no componente Pai comum mais próximo.

### 🗡️ Exemplo 5: useMemo para Cálculos Pesados
Se você tem uma lista de 1.000 aportes e faz uma soma total, use `useMemo` para não recalcular a soma a cada clique em qualquer outro botão.

### 🗡️ Exemplo 6: Context API (Dados Globais)
Use apenas para dados que o sistema INTEIRO precisa (Usuário Logado, Idioma, Permissões).

### 🗡️ Exemplo 7: Interceptores de API (Axios)
Crie um interceptor para anexar o Token JWT em todas as chamadas automaticamente. Não faça isso manualmente em cada componente.

### 🗡️ Exemplo 8: Custom Hooks (Reuso de Lógica)
```jsx
// Extraia a lógica complexa para hooks como useAuth ou useAportes.
function useAportes() {
    return useQuery(['aportes'], fetchAportes);
}
```

---

## 👨‍💻 Visão Sênior: O Vício no "useEffect"
Junior, o `useEffect` é para **Efeitos Colaterais** (sincronizar com sistemas fora do React, como uma biblioteca de gráficos ou uma conexão WebSocket). Se você está usando ele para calcular dados ou buscar da API, você provavelmente está complicando seu código. Use as ferramentas certas (React Query, useMemo).

---

## 💡 Próximos Passos
Treine sua arquitetura de Frontend:
[[Gerenciamento de Estado - Exercícios]]
