<template>
  <div class="slidev-layout" :class="{ 'with-background': background }">
    <slot> <h1>Index</h1> </slot>
    <ol>
      <li v-for="{ uri, title } in indexEntries" :key="title">
        <Link v-if="indexRedirectType === 'internal'" :to="uri">{{ title }}</Link>
        <TextWithOptionalLink v-else :link="uri" :text="title" />
      </li>
    </ol>
  </div>
</template>

<script setup lang="ts">
import { computed, PropType } from 'vue';

const background = $slidev.configs.background || false

const { indexEntries, indexRedirectType = 'internal' } = defineProps({
  indexEntries: {
    type: Array as PropType<{ title: string; uri?: number | string }[]>,
    required: true,
  },
  indexRedirectType: {
    type: String as PropType<'external' | 'internal'>,
    validator: (value) => value === 'external' || value === 'internal',
  },
});
</script>

<style>
.slidev-layout {
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
