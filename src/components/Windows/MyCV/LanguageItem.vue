<template>
  <div class="mt-2 mb-2">
    <p class="font-trebuchet-pixel text-xs">
      <span class="font-bold">{{ language.language }}</span>: {{ language.level }}
    </p>
  </div>
</template>

<script setup>
const props = defineProps({
  language: Object
})
</script>
