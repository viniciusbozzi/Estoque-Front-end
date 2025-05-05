<template>
  <div class="q-pa-md">
    <produto-form @dataUpdated="atualizarLista" />

    <produto-lista :key="atualizacaoKey" />
  </div>
</template>

<script setup>
import ProdutoForm from 'src/components/ProdutoForm.vue'
import ProdutoLista from 'src/components/ProdutoLista.vue'
import { ref } from 'vue'

const atualizacaoKey = ref(0)

const atualizarLista = () => {
  atualizacaoKey.value++
}
</script>
