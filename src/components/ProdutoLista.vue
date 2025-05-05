<template>
  <q-card flat bordered class="q-mt-md">
    <q-card-section>
      <div class="text-h6">Produtos Cadastrados</div>
    </q-card-section>
    <q-table :rows="produtos" :columns="columns" row-key="id" flat dense>
      <template v-slot:body-cell-actions="props">
        <q-td align="center">
          <q-btn color="negative" icon="delete" flat dense @click="excluir(props.row.id)" />
        </q-td>
      </template>
    </q-table>
  </q-card>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import { getLocalStorage, deleteData } from 'src/utils/utils'

const produtos = ref([])

const carregar = () => {
  produtos.value = getLocalStorage('produtos')
}

const excluir = (id) => {
  deleteData('produtos', id)
  carregar()
}

onMounted(carregar)

const columns = [
  { name: 'nome', label: 'Nome', field: 'nome', align: 'left' },
  { name: 'descricao', label: 'Descrição', field: 'descricao', align: 'left' },
  { name: 'actions', label: 'Ações', field: 'actions', align: 'center' },
]
</script>
