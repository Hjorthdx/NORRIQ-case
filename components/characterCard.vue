<template>
  <div class=" bg-gray-200 shadow-lg rounded-lg p-6 m-4 w-80 text-black">
    <h2 class="text-2xl font-bold mb-4">{{ character.name }}</h2>
    <div class="mb-4">
      <p><strong class="text-black">Height:</strong> {{ character.height }} cm</p>
      <p><strong class="text-black">Mass:</strong> {{ character.mass }} kg</p>
      <p><strong class="text-black">Birth Year:</strong> {{ character.birth_year }}</p>
      <p><strong class="text-black">Gender:</strong> {{ character.gender }}</p>
      <p><strong class="text-black">Number of Films:</strong> {{ character.films.length }}</p>
    </div>
    <div class="text-sm text-black">
      <p><strong class="text-black">Created:</strong> {{ new Date(character.created).toLocaleDateString() }}</p>
    </div>
  </div>
</template>

<script setup>
defineProps({
  character: Object
});
</script>
