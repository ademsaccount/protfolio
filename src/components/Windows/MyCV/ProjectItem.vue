<template>
  <div class="mt-2 mb-5">
    <h4 class="font-trebuchet-pixel uppercase text-xs">{{ project.name }}</h4>
    <p class="font-trebuchet-pixel text-xs">{{ project.description }}</p>
  </div>
</template>

<script setup>
const props = defineProps({
  project: Object
})
</script>
