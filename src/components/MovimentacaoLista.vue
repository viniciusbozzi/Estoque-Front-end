<template>
  <div class="q-pa-md">
    <q-table
      title="Movimentações"
      :rows="movimentacoesDetalhadas"
      :columns="columns"
      row-key="id"
      flat
      bordered
    >
      <template v-slot:body-cell-actions="props">
        <q-td align="center">
          <q-btn color="negative" flat icon="delete" @click="remover(props.row.id)" />
        </q-td>
      </template>
    </q-table>
  </div>
</template>

<script setup>
import { ref, onMounted, computed } from 'vue'
import { getLocalStorage, deleteData } from 'src/utils/utils'

// dados reativos
const movimentacoes = ref([])
const produtos = ref([])

// colunas da tabela
const columns = [
  { name: 'id', label: 'ID', field: 'id', align: 'left' },
  { name: 'produtoNome', label: 'Produto', field: 'produtoNome', align: 'left' },
  { name: 'tipo', label: 'Tipo', field: 'tipo', align: 'left' },
  { name: 'quantidade', label: 'Quantidade', field: 'quantidade', align: 'left' },
  { name: 'data', label: 'Data', field: 'data', align: 'left' },
  { name: 'actions', label: 'Ações', field: 'actions', align: 'center' },
]

// função para carregar dados do localStorage
const carregarDados = () => {
  movimentacoes.value = getLocalStorage('movimentacoes')
  produtos.value = getLocalStorage('produtos')
}

// computed para adicionar nome do produto
const movimentacoesDetalhadas = computed(() => {
  return movimentacoes.value.map((mov) => {
    const produto = produtos.value.find((p) => p.id === mov.produtoId) || {}
    return {
      ...mov,
      produtoNome: produto.nome || 'Desconhecido',
    }
  })
})

// função para remover movimentação
const remover = (id) => {
  deleteData('movimentacoes', id)
  carregarDados()
}

// carregar ao montar o componente
onMounted(carregarDados)
</script>
