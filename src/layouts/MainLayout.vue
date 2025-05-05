<template>
  <q-layout view="lHh Lpr lFf">
    <!-- Cabeçalho -->
    <q-header elevated>
      <q-toolbar>
        <q-btn flat dense round icon="menu" @click="drawer = !drawer" aria-label="Menu" />
        <q-toolbar-title>Sistema de Estoque</q-toolbar-title>
      </q-toolbar>
    </q-header>

    <!-- Menu lateral -->
    <q-drawer show-if-above v-model="drawer" side="left" bordered>
      <q-list>
        <q-item-label header>Navegação</q-item-label>

        <q-item clickable v-ripple to="/">
          <q-item-section avatar><q-icon name="home" /></q-item-section>
          <q-item-section>Início</q-item-section>
        </q-item>

        <q-item clickable v-ripple to="/produtos">
          <q-item-section avatar><q-icon name="inventory_2" /></q-item-section>
          <q-item-section>Produtos</q-item-section>
        </q-item>

        <q-item clickable v-ripple to="/movimentacoes">
          <q-item-section avatar><q-icon name="swap_horiz" /></q-item-section>
          <q-item-section>Movimentações</q-item-section>
        </q-item>

        <q-item clickable v-ripple to="/estoque">
          <q-item-section avatar><q-icon name="bar_chart" /></q-item-section>
          <q-item-section>Estoque</q-item-section>
        </q-item>
      </q-list>
    </q-drawer>

    <!-- Conteúdo principal -->
    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script setup>
import { ref } from 'vue'
const drawer = ref(true)
</script>
