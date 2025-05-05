<template>
  <div class="q-pa-md bg-grey-4">
    <q-form @submit="onSubmit" @reset="onReset" class="q-col-gutter-x-md">
      <div class="row q-col-gutter-md">
        <q-select
          filled
          bg-color="white"
          v-model="produtoId"
          :options="produtoOptions"
          label="Produto *"
          class="col-4"
          emit-value
          map-options
          option-label="nome"
          option-value="id"
        />

        <q-select
          filled
          bg-color="white"
          v-model="tipo"
          :options="['entrada', 'saida']"
          label="Tipo *"
          class="col-4"
        />

        <q-input
          filled
          bg-color="white"
          v-model.number="quantidade"
          type="number"
          label="Quantidade *"
          class="col-4"
        />
      </div>

      <div class="q-mt-md">
        <q-btn label="Salvar" type="submit" color="primary" />
        <q-btn label="Limpar" type="reset" color="primary" flat class="q-ml-sm" />
      </div>
    </q-form>
  </div>
</template>

<script setup>
import { ref, defineEmits, onMounted } from 'vue'
import { addNewData, getLocalStorage } from 'src/utils/utils'

const emit = defineEmits(['dataUpdated'])

const produtoId = ref(null)
const tipo = ref('')
const quantidade = ref(0)
const produtoOptions = ref([])
const movimentacoes = ref([])

onMounted(() => {
  produtoOptions.value = getLocalStorage('produtos')
  movimentacoes.value = getLocalStorage('movimentacoes') || []
})

const getEstoqueAtual = (produtoId) => {
  const entradas = movimentacoes.value
    .filter((m) => m.produtoId === produtoId && m.tipo === 'entrada')
    .reduce((soma, m) => soma + Number(m.quantidade), 0)

  const saidas = movimentacoes.value
    .filter((m) => m.produtoId === produtoId && m.tipo === 'saida')
    .reduce((soma, m) => soma + Number(m.quantidade), 0)

  return entradas - saidas
}

const onSubmit = () => {
  if (!produtoId.value || !tipo.value || !quantidade.value || quantidade.value <= 0) {
    alert('Preencha todos os campos corretamente.')
    return
  }

  if (tipo.value === 'saida') {
    const estoqueAtual = getEstoqueAtual(Number(produtoId.value))
    if (quantidade.value > estoqueAtual) {
      alert(`Estoque insuficiente! Estoque atual: ${estoqueAtual}`)
      return
    }
  }

  addNewData('movimentacoes', {
    produtoId: Number(produtoId.value),
    tipo: tipo.value,
    quantidade: Number(quantidade.value),
    data: new Date().toLocaleDateString(),
  })

  movimentacoes.value = getLocalStorage('movimentacoes') || []
  emit('dataUpdated')
  onReset()
}

const onReset = () => {
  produtoId.value = null
  tipo.value = ''
  quantidade.value = 0
}
</script>
