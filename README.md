# Cardapio Digital

Aplicacao em Vue 3 criada com `npm` e `Vite` para gerenciar o cardapio de uma lanchonete ficticia. O sistema permite cadastrar itens, filtrar por categoria, visualizar um resumo dinamico e remover produtos cadastrados.

## Como rodar

### Instalar dependencias

```bash
npm install
```

### Rodar em desenvolvimento

```bash
npm run dev
```

A aplicacao ficara disponivel no endereco mostrado pelo Vite, normalmente `http://localhost:5173`.

### Gerar build de producao

```bash
npm run build
```

## Funcionalidades

- Cadastro de itens com nome, preco, categoria e disponibilidade.
- Listagem dos itens em cards.
- Destaque visual para itens indisponiveis.
- Filtro por categoria com destaque do filtro ativo.
- Resumo com total de itens, total de disponiveis e preco medio visivel.
- Remocao de itens do cardapio.

## Estrutura dos componentes

- `App.vue`: componente pai que centraliza os dados do cardapio, os calculos e a comunicacao entre os componentes.
- `MenuForm.vue`: formulario de cadastro de novos itens.
- `MenuFilters.vue`: botoes de filtro por categoria.
- `MenuItens.vue`: exibicao dos cards e remocao dos itens.

## Conceitos do Vue aplicados

### `ref`

Usado em `src/App.vue` para armazenar estados principais da aplicacao:

- `itens`
- `filtroAtual` 

### `computed`

Usado em `src/App.vue` para dados derivados:

- `itensFiltrados`: filtra a lista de itens de acordo com a categoria selecionada
- `totalDisponiveis`: conta quantos itens estao disponiveis
- `precoMedioVisivel`: calcula o preco medio dos itens que estao visiveis no filtro atual

### `onMounted`

Usado em `src/App.vue` para carregar itens iniciais quando o componente e montado.

### `reactive`

Usado em `src/components/MenuForm.vue` para controlar os campos do formulario.

### `props`

Usado para enviar dados do componente pai para os filhos:

- `src/components/MenuFilters.vue` recebe `categorias` e `filtroAtual`
- `src/components/MenuItens.vue` recebe `itens`

### `emit`

Usado para o componente filho avisar o pai quando algo acontece:

- `src/components/MenuForm.vue` emite `add-item`
- `src/components/MenuFilters.vue` emite `change-filter`
- `src/components/MenuItens.vue` emite `remove-item`

### `v-model`

Usado em `src/components/MenuForm.vue` para ligar os campos do formulario ao estado reativo.

### `v-for`

Usado para renderizar listas:

- categorias em `src/components/MenuFilters.vue`
- itens em `src/components/MenuItens.vue`

### `v-if` e `v-else`

Usado em `src/components/MenuItens.vue` para mostrar a lista ou a mensagem de estado vazio.

### classes dinamicas

Usado para mudar o estilo conforme o estado:

- filtro ativo em `src/components/MenuFilters.vue`
- item indisponivel em `src/components/MenuItens.vue`

## Observacoes

- O `App.vue` ficou como dono dos dados, enquanto os componentes filhos recebem dados por `props` e se comunicam com ele usando `emit`.
