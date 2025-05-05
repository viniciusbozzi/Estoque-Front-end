<template>
  <div class="q-pa-md">
    <q-card>
      <q-card-section>
        <div class="row items-center justify-between">
          <div class="text-h6">Gráfico de Estoque</div>
          <q-select
            filled
            v-model="produtoSelecionado"
            :options="produtosOptions"
            label="Selecione o Produto"
            option-value="id"
            option-label="nome"
            emit-value
            map-options
            dense
            class="q-ml-md"
            style="width: 300px"
          />
        </div>
      </q-card-section>

      <q-separator />

      <q-card-section v-if="chartOptions">
        <v-chart :option="chartOptions" autoresize style="height: 400px" />
      </q-card-section>

      <q-card-section v-else>
        <q-banner dense class="bg-grey-2 text-grey-8">
          Nenhum dado disponível para o produto selecionado.
        </q-banner>
      </q-card-section>
    </q-card>
  </div>
</template>

<script setup>
import { ref, watchEffect } from 'vue'
import { getLocalStorage } from 'src/utils/utils'
import VChart from 'vue-echarts'
import { use } from 'echarts/core'
import { BarChart } from 'echarts/charts'
import {
  TitleComponent,
  TooltipComponent,
  GridComponent,
  LegendComponent,
} from 'echarts/components'
import { CanvasRenderer } from 'echarts/renderers'

use([BarChart, TitleComponent, TooltipComponent, GridComponent, LegendComponent, CanvasRenderer])

const produtos = ref([])
const movimentacoes = ref([])
const produtosOptions = ref([])
const produtoSelecionado = ref(null)
const chartOptions = ref(null)

watchEffect(() => {
  produtos.value = getLocalStorage('produtos')
  movimentacoes.value = getLocalStorage('movimentacoes')
  produtosOptions.value = produtos.value.map((p) => ({ id: p.id, nome: p.nome }))

  if (!produtoSelecionado.value && produtosOptions.value.length > 0) {
    produtoSelecionado.value = produtosOptions.value[0].id
  }

  if (produtoSelecionado.value) {
    const produto = produtos.value.find((p) => p.id === produtoSelecionado.value)

    const entradas = movimentacoes.value
      .filter((m) => Number(m.produtoId) === produtoSelecionado.value && m.tipo === 'entrada')
      .reduce((sum, m) => sum + Number(m.quantidade), 0)

    const saidas = movimentacoes.value
      .filter((m) => Number(m.produtoId) === produtoSelecionado.value && m.tipo === 'saida')
      .reduce((sum, m) => sum + Number(m.quantidade), 0)

    chartOptions.value = {
      tooltip: { trigger: 'axis' },
      legend: { data: ['Entradas', 'Saídas', 'Estoque Atual'] },
      xAxis: {
        type: 'category',
        data: [produto.nome],
      },
      yAxis: { type: 'value' },
      series: [
        {
          name: 'Entradas',
          type: 'bar',
          data: [entradas],
          itemStyle: { color: '#4caf50' },
        },
        {
          name: 'Saídas',
          type: 'bar',
          data: [saidas],
          itemStyle: { color: '#f44336' },
        },
        {
          name: 'Estoque Atual',
          type: 'bar',
          data: [entradas - saidas],
          itemStyle: { color: '#2196f3' },
        },
      ],
    }
  } else {
    chartOptions.value = null
  }
})
</script>
