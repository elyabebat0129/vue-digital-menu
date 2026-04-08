' '<script setup>
import { reactive } from 'vue'

const emit = defineEmits(['add-item'])

const form = reactive({
  nome: '',
  preco: null,
  categoria: 'Lanche',
  disponivel: true,
})

const resetarFormulario = () => {
  form.nome = ''
  form.preco = null
  form.categoria = 'Lanche'
  form.disponivel = true
}

const enviarFormulario = () => {
  emit('add-item', {
    nome: form.nome.trim(),
    preco: Number(form.preco),
    categoria: form.categoria,
    disponivel: form.disponivel,
  })

  resetarFormulario()
}
</script>

<template>
  <section class="bloco">
    <h2>Cadastro de itens</h2>

    <form class="formulario" @submit.prevent="enviarFormulario">
      <input v-model="form.nome" type="text" placeholder="Nome do item" required />

      <input
        v-model.number="form.preco"
        type="number"
        min="0"
        step="0.01"
        placeholder="Preco"
        required
      />

      <select v-model="form.categoria">
        <option value="Lanche">Lanche</option>
        <option value="Bebida">Bebida</option>
        <option value="Sobremesa">Sobremesa</option>
      </select>

      <label class="checkbox">
        <input v-model="form.disponivel" type="checkbox" />
        Disponivel
      </label>

      <button type="submit">Adicionar item</button>
    </form>
  </section>
</template>

<style scoped>
.bloco {
  margin-bottom: 24px;
}

.formulario {
  display: grid;
  gap: 12px;
}

.checkbox {
  display: flex;
  gap: 8px;
  align-items: center;
}
</style>
