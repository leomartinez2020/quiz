<template>
  <div class="bg-white shadow-lg rounded-lg p-6 mb-4 w-full max-w-md text-center">
    <p class="text-xl font-semibold">{{ question }}</p>
  </div>
</template>

<script setup>
defineProps({
  question: {
    type: String,
    required: true
  }
})
</script>

<style>
.text-xl {
  font-size: 2em;
}
</style>
