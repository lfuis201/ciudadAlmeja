<template>
    <main class="flex items-center justify-center h-screen w-screen bg-gradient-to-b from-[#23617d] to-[#112031] relative">
      <ul class="light-rays absolute w-full h-full top-0 left-0 pointer-events-none blur-lg">
        <li v-for="i in 32" :key="i" :style="getStyle(i)"></li>
      </ul>
      <div class="login relative z-10 p-4 -mt-32 flex flex-col items-center">
        <h1 class="font-teko text-5xl text-center text-transparent bg-gradient-to-b from-white to-[#7ff] bg-clip-text opacity-80">
          Ocean Voyage
        </h1>
        <form @submit.prevent class="grid grid-cols-1 md:grid-cols-2 gap-4 p-8 bg-white bg-opacity-10 shadow-inner text-white">
          <div class="group flex flex-col">
            <label for="email" class="text-right opacity-70">Email</label>
            <input type="email" id="email" class="border-none rounded p-2 bg-white bg-opacity-30 focus:bg-opacity-50 transition" />
          </div>
          <div class="group flex flex-col">
            <label for="password" class="text-right opacity-70">Password</label>
            <input type="password" id="password" class="border-none rounded p-2 bg-white bg-opacity-30 focus:bg-opacity-50 transition" />
          </div>
          <button type="submit" class="col-span-2 bg-white bg-opacity-30 text-white text-xl uppercase py-2 hover:bg-opacity-50 transition">
            Login
          </button>
        </form>
      </div>
    </main>
  </template>
  
  <script setup lang="ts">
  import { ref } from 'vue';
  
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
  @import url("https://fonts.googleapis.com/css2?family=Teko&display=swap");
  
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
  