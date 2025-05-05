# 📦 Controle de Estoque - Vue.js + Quasar

Este é um projeto de controle de estoque simples, desenvolvido com **Vue 3**, **Quasar Framework** e armazenamento em **localStorage**. O sistema permite:

- Cadastro de produtos
- Registro de movimentações de entrada e saída
- Validação de estoque disponível
- Visualização de gráfico de movimentações por produto

🔗 Repositório: [github.com/viniciusbozzi/Estoque-Front-end](https://github.com/viniciusbozzi/Estoque-Front-end)

# Estrutura do projeto

```bash
src/
├── components/
│   ├── ProdutoForm.vue
│   ├── ProdutoLista.vue
│   ├── MovimentacaoForm.vue
│   ├── MovimentacaoLista.vue
│   └── EstoqueGrafico.vue
├── pages/
│   ├── IndexPage.vue
│   ├── ProdutoPage.vue
│   ├── MovimentacaoPage.vue
│   └── EstoquePage.vue
├── utils/
│   └── utils.js   # Funções genéricas para localStorage
└── App.vue
```

---

## 🚀 Tecnologias Utilizadas

- [Vue 3](https://vuejs.org/)
- [Quasar Framework](https://quasar.dev/)
- [ECharts](https://echarts.apache.org/) via `vue-echarts` (para os gráficos)
- `localStorage` (persistência de dados local)

---

## ⚙️ Pré-requisitos

- [Node.js](https://nodejs.org/) instalado (recomendado: versão 22)
- [npm](https://www.npmjs.com/) (versão 10) como gerenciador de pacotes

- [Quasar CLI](https://quasar.dev/start/quasar-cli) instalado globalmente, faça:

```bash
npm install -g @quasar/cli
```

---

## 📦 Instalação

```bash
# 1. Clone o repositório
git clone https://github.com/viniciusbozzi/Estoque-Front-end.git

# 2. Acesse a pasta do projeto
cd Estoque-Front-end

# 3. Instale as dependências
npm install

# 4. Instale dependências para gráficos
npm install echarts vue-echarts
```

# Inicie o servidor de desenvolvimento

```bash
quasar dev
```

# Testando a Aplicação

Acesse o sistema via navegador. (http://localhost:9000/#/)

Cadastre um produto.

Registre movimentações de entrada e saída.

Tente registrar uma saída maior que o estoque e veja a validação.

Visualize o gráfico do estoque do produto.
