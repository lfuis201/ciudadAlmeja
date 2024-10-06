<script setup lang="ts">
import { RouterView } from "vue-router";
</script>

<template>
  <div class="custom-cursor"> <!-- Aplicar la clase aquí -->
    <router-view />
    <!-- Aquí van tus componentes hijos -->
  </div>
</template>

<style scoped>
.custom-cursor {
  cursor: url('../src/assets/img/subRIGHT.png'), auto; /* Usando la alias @ para la ruta */
}
</style>
