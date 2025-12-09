<template>
  <div class="slidev-layout cover" :class="{ 'with-background': background }" :style="style">
    <div class="my-auto w-full">
      <slot />
      <div v-if="coverAuthors.length || coverDate" class="absolute bottom-12 flex">
        <p v-if="coverAuthors.length">
          <template v-for="(coverAuthor, idx) in coverAuthors">
            <TextWithOptionalLink :link="coverAuthorUrls[idx]" :text="coverAuthor" />
            <span v-if="idx < coverAuthors.length - 2">, </span>
            <span v-if="idx === coverAuthors.length - 2"> and </span>
          </template>
        </p>
        <p v-if="coverDate">{{ coverAuthors.length ? `, ${coverDate}` : coverDate }}</p>
      </div>
      <div class="absolute bottom-0 font-extralight mb-1 mr-2 right-0 text-xs" v-if="coverBackgroundSource">
        <TextWithOptionalLink :link="coverBackgroundSourceUrl" :text="coverBackgroundSource" />
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { computed } from 'vue';
import { handleBackground } from '../layout-helper';

const {
  coverAuthor: coverAuthorTransferred,
  coverAuthorUrl: coverAuthorUrlTransferred,
  coverBackgroundUrl,
  coverDate = new Date().toLocaleDateString(),
} = defineProps<{
  coverAuthor?: string | string[];
  coverAuthorUrl?: string | string[];
  coverBackgroundUrl?: string;
  coverBackgroundSource?: string;
  coverBackgroundSourceUrl?: string;
  coverDate?: string | Date;
}>();

const background = $slidev.configs.background || false
const coverAuthors = computed(() => transformIntoArray(coverAuthorTransferred));
const coverAuthorUrls = computed(() => transformIntoArray(coverAuthorUrlTransferred));
const style = computed(() => handleBackground(coverBackgroundUrl, true));

const transformIntoArray = (value: string | string[] | undefined) => {
  if (Array.isArray(value)) return value;
  if (!value) return [];
  return [value];
};
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
