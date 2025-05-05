<template>
  <div class="q-pa-md">
    <movimentacao-form @dataUpdated="atualizarLista" />
    <movimentacao-lista :key="atualizacaoKey" />
  </div>
</template>

<script setup>
import MovimentacaoForm from 'src/components/MovimentacaoForm.vue'
import MovimentacaoLista from 'src/components/MovimentacaoLista.vue'
import { ref } from 'vue'

const atualizacaoKey = ref(0)

const atualizarLista = () => {
  atualizacaoKey.value++
}
</script>
