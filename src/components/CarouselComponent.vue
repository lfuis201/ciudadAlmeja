<template>

<div class="text-center mb-8">
    <h1 class="inline-block bg-gray-300 p-4 rounded-full text-4xl font-bold">Título Titulo</h1>
  </div>
  

    <Carousel v-bind="settings" :breakpoints="breakpoints">
      <Slide v-for="slide in slides" :key="slide">
        <div class="carousel__item bg-green-500 flex justify-center items-center h-64 w-64 text-white text-2xl font-bold">
            {{ slide }}
        </div>
      </Slide>
  
      <!-- Controles de navegación -->
      <template #addons>
        <Navigation />
      </template>
    </Carousel>
  </template>
  
  <script setup lang="ts">
  import { ref, reactive } from 'vue';
  import { Carousel, Navigation, Slide } from 'vue3-carousel';
  import 'vue3-carousel/dist/carousel.css';
  
  // Configuración del carrusel
  const settings = reactive({
    itemsToShow: 1,
    snapAlign: 'center',
  });
  
  // Breakpoints para comportamiento responsive
  const breakpoints = reactive({
    700: {
      itemsToShow: 3.5,
      snapAlign: 'center',
    },
    1024: {
      itemsToShow: 3,
      snapAlign: 'start',
    },
  });
  
  // Definir las diapositivas (slides)
  const slides = ref(Array.from({ length: 10 }, (_, i) => i + 1));
  </script>
  
  <style scoped>
  /* Clase de fondo para cada slide está aplicada en el template con Tailwind (bg-green-500) */
  /* Si quieres estilos adicionales los puedes agregar aquí */
  </style>
  