<template>
  <div class="flex h-full with-background" :class="{ 'with-background': background }">
    <div class="slidev-layout default flex-1">
      <slot />
    </div>
    <FigureWithOptionalCaption
      class="flex-1 h-4/5 m-auto px-4"
      :class="{
        'order-first': figureX === 'l',
      }"
      :caption="figureCaption"
      :footnoteNumber="figureFootnoteNumber"
      :url="figureUrl"
    />
  </div>
</template>

<script setup lang="ts">
const background = $slidev.configs.background || false

withDefaults(
  defineProps<{
    figureCaption?: string;
    figureFootnoteNumber?: number;
    figureUrl: string;
    figureX?: 'l' | 'r';
  }>(),
  { figureX: 'r' },
);
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
