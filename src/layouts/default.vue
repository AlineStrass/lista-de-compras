<template>
  <v-app id="inspire">
    <v-app-bar>
      <!-- ICONE -->
      <v-app-bar-nav-icon @click="drawer = !drawer"></v-app-bar-nav-icon>
      <!-- NOME DO APP -->
      <v-app-bar-title>Lista de Compras</v-app-bar-title>
    </v-app-bar>
    <!-- CORPO DO SITE -->
    <v-main>
      <router-view></router-view>
    </v-main>
  </v-app>
</template>

<script setup>
  import { ref } from 'vue'
  const drawer = ref(0)
</script>


