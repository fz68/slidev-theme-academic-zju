<template>
  <div class="slidev-layout intro" :class="{ 'with-background': background }">
    <div class="my-auto">
      <slot />
    </div>
  </div>
</template>

<script setup>
const background = $slidev.configs.background || false
</script>

<style>
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
