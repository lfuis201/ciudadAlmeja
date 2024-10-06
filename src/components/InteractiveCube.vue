<template>
  <div class="relative w-full h-screen flex justify-center items-center">
    <!-- Contenedor de Three.js -->
    <div ref="threeCanvas" class="three-canvas"></div>

    <!-- Mensaje de información -->
    <h1
      v-if="state.clicked"
      class="info-text bg-black/70 text-white text-lg p-4 rounded-md absolute top-5 left-5"
    >
      ¡Hiciste clic en el modelo! Información: Rotación X: {{ modelRotationX.toFixed(2) }} | Rotación Y: {{ modelRotationY.toFixed(2) }}
    </h1>
  </div>
</template>

<script setup lang="ts">
import { onMounted, ref, reactive, computed } from "vue";
import {
  Scene,
  PerspectiveCamera,
  WebGLRenderer,
  Raycaster,
  Vector2,
  AmbientLight,
  DirectionalLight,
} from "https://cdn.jsdelivr.net/npm/three@0.153.0/build/three.module.js";
import { GLTFLoader } from "https://cdn.jsdelivr.net/npm/three@0.153.0/examples/jsm/loaders/GLTFLoader.js";
import { OrbitControls } from "https://cdn.jsdelivr.net/npm/three@0.153.0/examples/jsm/controls/OrbitControls.js"; // Importar OrbitControls

// Referencias y estado reactivo
const threeCanvas = ref(null);
let scene, camera, renderer, model, controls;
const state = reactive({ clicked: false });

// Variables para la rotación del modelo
const modelRotationX = computed(() => (model ? model.rotation.x : 0));
const modelRotationY = computed(() => (model ? model.rotation.y : 0));

// Raycaster y vector de posición
const raycaster = new Raycaster();
const mouse = new Vector2();

onMounted(() => {
  // Dimensiones del canvas
  const width = window.innerWidth;
  const height = window.innerHeight;

  // Crear la escena
  scene = new Scene();

  // Crear la cámara
  camera = new PerspectiveCamera(60, width / height, 0.1, 100);
  camera.position.set(0, 0, 5); // Posición inicial de la cámara

  // Crear el renderizador
  renderer = new WebGLRenderer();
  renderer.setSize(width, height);
  renderer.setClearColor(0xffffff); // Fondo blanco

  // Añadir el renderizador al DOM
  if (threeCanvas.value) {
    threeCanvas.value.appendChild(renderer.domElement);
  }

  // Añadir luces a la escena
  const ambientLight = new AmbientLight(0x404040); // Luz ambiental suave
  scene.add(ambientLight);

  const directionalLight = new DirectionalLight(0xffffff, 1); // Luz direccional blanca
  directionalLight.position.set(5, 5, 5); // Posición de la luz
  scene.add(directionalLight);

  // Cargar el modelo GLB
  const loader = new GLTFLoader();
  loader.load(
    new URL('../assets/sea_shack.glb', import.meta.url).href,
    (gltf) => {
      model = gltf.scene; // Obtener el objeto 3D
      model.scale.set(0.001, 0.001, 0.001); // Escalar el modelo
      scene.add(model); // Añadir el modelo a la escena
    },
    undefined,
    (error) => {
      console.error('Error cargando el modelo GLB:', error);
    }
  );

  // Inicializar OrbitControls
  controls = new OrbitControls(camera, renderer.domElement);
  controls.enableDamping = true; // Habilitar amortiguamiento
  controls.dampingFactor = 0.25;
  controls.screenSpacePanning = false;
  controls.maxDistance = 10;
  controls.minDistance = 1;

  // Manejar el evento de clic
  window.addEventListener("click", onMouseClick);

  // Función de animación
  const animate = () => {
    requestAnimationFrame(animate);

    // Actualizar controles
    controls.update(); // Actualizar controles en cada frame

    // Renderizar la escena
    renderer.render(scene, camera);
  };

  // Iniciar la animación
  animate();
});

// Función para manejar el clic
function onMouseClick(event) {
  // Calcular la posición del mouse en coordenadas normalizadas
  mouse.x = (event.clientX / window.innerWidth) * 2 - 1;
  mouse.y = -(event.clientY / window.innerHeight) * 2 + 1;

  // Actualizar el raycaster con la cámara y la posición del mouse
  raycaster.setFromCamera(mouse, camera);

  // Calcular los objetos intersectados
  const intersects = raycaster.intersectObjects(scene.children);

  if (intersects.length > 0) {
    state.clicked = !state.clicked; // Alternar el estado del clic

    const intersectedObject = intersects[0].object;

    // Alternar el color entre verde y rojo
    if (intersectedObject.material.color.getHex() === 0xff0000) {
      intersectedObject.material.color.set(0x00ff00); // Cambiar a verde
    } else {
      intersectedObject.material.color.set(0xff0000); // Cambiar a rojo
    }
  }
}
</script>

<style scoped>
.three-canvas {
  width: 100vw;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  overflow: hidden;
}

.info-text {
  position: absolute;
  top: 20px;
  left: 20px;
  color: white;
  padding: 10px;
  border-radius: 5px;
}
</style>
