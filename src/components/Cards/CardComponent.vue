<template>
  <div class="flex flex-row items-center">
    <!-- Imagen circular a la izquierda -->
    <div
      class="relative w-64 h-64 rounded-full bg-blue-300 overflow-hidden mr-24"
    >
      <img
        class="w-full h-full object-cover"
        src="https://tecdn.b-cdn.net/wp-content/uploads/2020/06/vertical.jpg"
        alt=""
      />
    </div>

    <!-- Contenedor de la tarjeta, a la derecha de la imagen -->
    <div
      class="flex flex-col justify-between rounded-lg bg-white text-surface shadow-secondary-1 dark:bg-surface-dark dark:text-white md:max-w-xl ml-24 h-64"
      style="width: 80rem"
    >
      <div class="flex flex-col justify-start p-6 h-full">
        <!-- Ajusta para que ocupe el 100% de la altura -->
        <!-- Título centrado con fondo redondeado -->
        <div class="flex justify-center mb-4 p-4 bg-gray-200 rounded-full w-1/2 mx-auto">
        <h5 class="text-xl text-black font-medium text-center">
          Título Centrados
        </h5>
      </div>

        <p class="mb-4 text-base text-black">
          This is a wider card with supporting text below as a natural lead-in
          to additional content. This content is a little bit longer.
        </p>
        <p class="text-xs text-black text-surface/75 dark:text-neutral-300">
          Last updated 3 mins ago
        </p>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
// No es necesario incluir lógica específica en este ejemplo.
</script>

<style scoped>
/* Agrega cualquier estilo adicional que quieras aplicar al componente aquí */
</style>
