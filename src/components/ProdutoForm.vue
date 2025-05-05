<template>
  <div class="q-pa-md bg-grey-4">
    <q-form @submit="onSubmit" @reset="onReset" class="q-col-gutter-x-md">
      <div class="row q-col-gutter-md">
        <q-input filled bg-color="white" v-model="nome" label="Nome *" class="col-6" />
        <q-input filled bg-color="white" v-model="descricao" label="Descrição *" class="col-6" />
      </div>
      <div class="q-mt-md">
        <q-btn label="Salvar" type="submit" color="primary" />
        <q-btn label="Limpar" type="reset" color="primary" flat class="q-ml-sm" />
      </div>
    </q-form>
  </div>
</template>

<script setup>
import { ref, defineEmits } from 'vue'
import { addNewData } from 'src/utils/utils'

const emit = defineEmits(['dataUpdated'])

const nome = ref('')
const descricao = ref('')

const onSubmit = () => {
  addNewData('produtos', {
    nome: nome.value,
    descricao: descricao.value,
  })
  emit('dataUpdated')
  onReset()
}

const onReset = () => {
  nome.value = ''
  descricao.value = ''
}
</script>
