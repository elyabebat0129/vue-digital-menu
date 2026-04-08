<script setup>
import { computed, onMounted, ref } from 'vue'
import MenuFilters from './components/MenuFilters.vue'
import MenuForm from './components/MenuForm.vue'
import MenuItens from './components/MenuItens.vue'

const itens = ref([])
const filtroAtual = ref('Todas')

const categorias = ['Todas', 'Lanche', 'Bebida', 'Sobremesa']

const itensFiltrados = computed(() => {
  if (filtroAtual.value === 'Todas') {
    return itens.value
  }

  return itens.value.filter((item) => item.categoria === filtroAtual.value)
})

const totalDisponiveis = computed(() => {
  return itens.value.filter((item) => item.disponivel).length
})

const precoMedioVisivel = computed(() => {
  if (itensFiltrados.value.length === 0) {
    return 0
  }

  const soma = itensFiltrados.value.reduce((acumulador, item) => {
    return acumulador + item.preco
  }, 0)

  return soma / itensFiltrados.value.length
})

const adicionarItem = (novoItem) => {
  itens.value.push({
    id: Date.now(),
    ...novoItem,
  })
}

const removerItem = (id) => {
  itens.value = itens.value.filter((item) => item.id !== id)
}

onMounted(() => {
  itens.value = [
    {
      id: 1,
      nome: 'X-Burguer',
      preco: 22,
      categoria: 'Lanche',
      disponivel: true,
    },
    {
      id: 2,
      nome: 'Refrigerante',
      preco: 8,
      categoria: 'Bebida',
      disponivel: false,
    },
    {
      id: 3,
      nome: 'Petit Gateau',
      preco: 18,
      categoria: 'Sobremesa',
      disponivel: true,
    },
  ]
})
</script>

<template>
  <main class="container">
    <h1>Cardapio Digital</h1>

    <section class="bloco">
      <h2>Resumo</h2>
      <p>Total de itens: {{ itens.length }}</p>
      <p>Itens disponiveis: {{ totalDisponiveis }}</p>
      <p>Preco medio visivel: R$ {{ precoMedioVisivel.toFixed(2) }}</p>
    </section>

    <MenuForm @add-item="adicionarItem" />

    <MenuFilters />

    <MenuItens />
  </main>
</template>

<style scoped>
.container {
  max-width: 900px;
  margin: 0 auto;
  padding: 24px;
}

.bloco {
  margin-bottom: 24px;
}
</style>
