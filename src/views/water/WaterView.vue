<script setup lang="ts">
import UnderWaterLayout from '@/layouts/UnderWaterLayout.vue';
import { onMounted } from 'vue';
import $ from 'jquery';
import 'jquery.ripples';  // Importa el plugin de ripples

import InteractiveCube from '@/components/InteractiveCube.vue';
import WaterLayout from '@/layouts/WaterLayout.vue';

// Aplica el efecto ripples cuando el componente se monte
onMounted(() => {
  $(".full-landing-image").ripples({
    resolution: 512,
    dropRadius: 20,
    perturbance: 0.04,
  });
});
</script>

<template>
  <WaterLayout>
    <!-- Custom content that will be injected into the layout -->
    <div class="flex items-center justify-center h-full">
      <h1 class="title">Welcome to the Underwater World</h1> <!-- Aplica la clase title aquí -->
    </div>
  </WaterLayout>
  <UnderWaterLayout />
  <InteractiveCube />
</template>

<style scoped>
body {
  margin: 0;
  padding: 0;
}

.full-landing-image {
  width: 100%;
  height: 100vh;
  background: url('@/assets/img/font1.jpg') no-repeat center;
  background-size: cover;
}

/* Estilo específico para el título */
.title {
  font-family: "Orbitron", sans-serif; /* Aplica la fuente Orbitron al título */
  font-weight: 700;
  color: transparent; /* Color del texto interno (transparente) */
  font-size: 8rem; /* Aumenta el tamaño del título */
  text-align: center;
  text-shadow: 
    0 0 5px white, /* Sombra blanca para crear el borde */
    0 0 10px white; /* Aumenta la visibilidad del borde */
}
</style>
