<template>
    <div class="flex justify-center space-x-4 mb-4">
      <label class="flex items-center space-x-2">
        <input type="checkbox" v-model="filters.male" class="form-checkbox h-4 w-4 text-blue-600">
        <span>Show only males</span>
      </label>
      <label class="flex items-center space-x-2">
        <input type="checkbox" v-model="filters.female" class="form-checkbox h-4 w-4 text-blue-600">
        <span>Show only females</span>
      </label>
      <label class="flex items-center space-x-2">
        <input type="checkbox" v-model="filters.birthYear" class="form-checkbox h-4 w-4 text-blue-600">
        <span>Show only characters born between 20 and 40 BBY</span>
      </label>
    </div>
</template>
  
<script setup>
  defineProps({
    filters: Object
  });
</script>
  