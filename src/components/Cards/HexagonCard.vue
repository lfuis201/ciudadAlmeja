<template>
    <div class="h-screen flex items-center justify-center">
      <div class="w-full max-w-screen-lg glassmorphism border border-gray-300 rounded-lg shadow-lg overflow-hidden">
        <div class="bg-transparent p-4">
          <h2 class="text-lg font-semibold text-primary truncate text-center">RESPIRADORES HIDROTERMALES</h2>
        </div>
        <div class="flex justify-center items-center p-4">
          <div class="w-16 h-16 bg-accent rounded-full flex items-center justify-center">
            <span class="text-accent-foreground">🌊</span>
          </div>
        </div>
      </div>
    </div>
  </template>
  
  <script setup lang="ts">
  // Aquí puedes agregar cualquier lógica adicional si es necesario.
  </script>
  
  <style scoped>
  .glassmorphism {
    backdrop-filter: blur(9px) saturate(200%);
    -webkit-backdrop-filter: blur(9px) saturate(200%);
    background-color: rgba(17, 25, 40, 0.29);
    border-radius: 12px;
    border: 1px solid rgba(255, 255, 255, 0.125);
  }
  </style>
  