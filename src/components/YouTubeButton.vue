<template>
  <a
    :href="href"
    target="_blank"
    class="px-3 py-2 rounded border-2 bg-red-600 text-white border-red-600 hover:bg-red-700 transition-colors"
    >Youtube</a
  >
</template>

<script setup>
const props = defineProps({
  href: String,
});
</script>
