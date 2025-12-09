<template>
  <div class="slidev-layout default h-full" :class="{ 'with-background': background }">
    <slot />
    <FigureWithOptionalCaption
      class="h-5/6 p-4"
      :caption="figureCaption"
      :footnoteNumber="figureFootnoteNumber"
      :url="figureUrl"
    />
  </div>
</template>

<script setup lang="ts">
const background = $slidev.configs.background || false

defineProps<{
  figureCaption?: string;
  figureFootnoteNumber?: number;
  figureUrl: string;
}>();
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
