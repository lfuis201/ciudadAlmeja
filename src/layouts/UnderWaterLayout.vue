<template>
  <!-- Primera capa con Tailwind para ocupar toda la pantalla -->
  <div class="layer-1 flex items-center justify-center h-screen w-full custom-cursor">
    <!-- Contenido adicional aquí si es necesario -->
  </div>

  <!-- Segunda capa con la animación de rayos -->
  <div class="layer-2 w-full relative">
    <ul class="light-rays absolute w-full h-full top-0 left-0 pointer-events-none blur-lg">
        <li v-for="i in 32" :key="i" :style="getStyle(i)"></li>
      </ul>
    <CarouselComponent />
  </div>

  <div class="layer-3 h-screen w-full">
    <div class="flex flex-col items-center justify-center space-y-4 p-4 h-screen">
      <CardComponent v-for="index in 2" :key="index" />
    </div>
  </div>

  <div class="layer-4 w-full">
    <!-- Contenido adicional aquí si es necesario -->
  </div>

  <div class="layer-5 w-full">
    <div class="flex flex-col items-center p-16">
      <!-- Título -->
      <h2 class="bg-black text-white py-2 px-4 rounded-full mb-4">
        CARACTERISTICAS GEOLÓGICAS
      </h2>

      <!-- Contenedor para las tarjetas en grid -->
      <div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 gap-4 w-full">
        <div class="bg-zinc-300 p-4 rounded-lg shadow-md h-64 flex items-center justify-center">
          <h3 class="text-center font-semibold">PROCESOS GEOLOGICOS</h3>
        </div>
        <div class="bg-zinc-300 p-4 rounded-lg shadow-md h-64 flex items-center justify-center">
          <h3 class="text-center font-semibold">COMPOSICIÓN MINERAL</h3>
        </div>
        <div class="bg-zinc-300 p-4 rounded-lg shadow-md h-64 flex items-center justify-center">
          <h3 class="text-center font-semibold">CAPAS DEL PLANETA</h3>
        </div>
      </div>
    </div>

    <HexagonCard />
  </div>
</template>

<script setup lang="ts">
import { defineComponent, ref } from "vue";
import CarouselComponent from "@/components/CarouselComponent.vue";
import CardComponent from "@/components/Cards/CardComponent.vue";
import HexagonCard from "@/components/Cards/HexagonCard.vue";

  // Función para generar estilos aleatorios
  const getStyle = (index: number) => {
    const deg = Math.random();
    const thickness = `${8 + Math.random() * 26}px`;
    const length = `${-50 + Math.random() * 100}px`;
    const duration = `${1 + Math.random() * 1.5}s`;
    const delay = `${2 + Math.random() * 1}s`;
    const rotate = `${-4 + Math.random() * 8}deg`;
  
    return {
      '--deg': deg,
      '--thickness': thickness,
      '--length': length,
      '--duration': duration,
      '--delay': delay,
      '--rotate': rotate,
    };
  };
</script>

<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Orbitron:wght@400..900&family=Teko:wght@300..700&display=swap");

/* Gradientes personalizados para cada layer */
.layer-1 {
  background: linear-gradient(to bottom, #001c28, rgba(0, 204, 255, 0.8)); /* Azul claro */
}

.layer-2 {
  background: linear-gradient(to bottom, rgba(0, 204, 255, 0.8), rgba(0, 153, 255, 0.9)); /* Azul más profundo */
  position: relative; /* Para que los rayos se coloquen correctamente */
}

.layer-3 {
  background: linear-gradient(to bottom, rgba(0, 153, 255, 0.9), rgba(0, 102, 204, 0.7)); /* Azul intenso */
}

.layer-4 {
  background: linear-gradient(to bottom, rgba(0, 102, 204, 0.7), rgba(0, 51, 153, 0.8)); /* Azul oscuro */
}

.layer-5 {
  background: linear-gradient(to bottom, rgba(0, 51, 153, 0.8), rgba(0, 0, 102, 0.9)); /* Azul marino */
}

/* Estilo para el título */
.title {
  font-family: "Orbitron", sans-serif; /* Aplica la fuente Orbitron al título */
  font-weight: 700;
  color: white;
  text-align: center;
  font-size: 6rem;
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.5);
}
.light-rays {
    position: absolute;
    display: block;
    width: 100%;
    height: 100%;
    top: 0;
    left: 0;
    pointer-events: none;
    filter: blur(0.6rem);
  }
  
  .light-rays li {
    position: absolute;
    transform-style: preserve-3d;
    perspective: 500px;
    width: var(--thickness, 20px);
    height: calc(20% + 370px + var(--length, 0rem));
    left: 50%;
    transform: translateX(
        calc(
          -50% + var(--deg) * 40vw * -1 + 0.5 * 40vw
        )
      )
      translateY(-100px)
      rotateZ(calc(72.5deg * -0.5 + var(--deg) * 72.5deg))
      rotateX(0.01deg);
    transform-origin: center -100px;
    mix-blend-mode: screen;
    animation: shimmer linear var(--duration, 2s) calc(var(--delay, 1s) * -1) infinite alternate forwards,
      rotate ease-in-out calc(var(--duration, 2s) * 3.14) calc(var(--delay, 1s) * -1) infinite alternate forwards;
  
    &::before {
      content: "";
      position: absolute;
      width: 100%;
      height: 100%;
      background: linear-gradient(
        to bottom,
        rgba(166, 255, 248, 1),
        rgba(166, 255, 248, 0) 100%
      );
      transform-origin: top center;
      transform: rotateX(40deg);
    }
  }
  
  @keyframes shimmer {
    0% {
      opacity: 0.33;
    }
  
    100% {
      opacity: 0.03;
    }
  }
  
  @keyframes rotate {
    0% {
      rotate: 0deg;
    }
  
    100% {
      rotate: var(--rotate);
    }
  }

</style>
