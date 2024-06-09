<template>
  <div class="flex flex-wrap justify-center">
    <CharacterCard
      v-for="character in filteredCharacters"
      :key="character.url"
      :character="character"
      :loading="loading"
    />
    <SkeletonCard v-if="loading" v-for="n in 10" :key="'skeleton-' + n" />
  </div>
</template>

<script setup>
defineProps({
  filteredCharacters: Array,
  loading: Boolean,
  cardsInRow: Number
});
</script>
