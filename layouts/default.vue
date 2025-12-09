<template>
  <div class="slidev-layout default" :class="{ 'with-background': background }">
    <div class="w-full h-full">
      <slot />
    </div>
  </div>
</template>

<script setup>
const background = $slidev.configs.background || false
</script>

<style>
.slidev-layout.default {
  display: flex;
  flex-direction: column;
}

.with-background {
  background-image: url('../assets/zju.jpg') !important;
  background-size: cover !important;
  background-position: center !important;
  background-repeat: no-repeat !important;
  position: relative !important;
}

.with-background::before {
  content: "" !important;
  position: absolute !important;
  top: 0 !important;
  left: 0 !important;
  right: 0 !important;
  bottom: 0 !important;
  background: rgba(255, 255, 255, 0.1) !important;
  z-index: -1 !important;
}
</style>