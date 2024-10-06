<script setup lang="ts">
import { onMounted } from 'vue';
import $ from 'jquery';
import 'jquery.ripples';  // Import the ripples plugin

// Apply the ripple effect when the component is mounted
onMounted(() => {
  $(".full-landing-image").ripples({
    resolution: 512,
    dropRadius: 20,
    perturbance: 0.04,
  });
});
</script>

<template>
  <div class="full-landing-image relative overflow-hidden">
    <!-- Slot for injecting dynamic content into this layout -->
    <slot></slot>
  </div>
</template>

<style scoped>
.full-landing-image {
  background: url('@/assets/img/font1.jpg') no-repeat center;
  background-size: cover;
}
</style>
