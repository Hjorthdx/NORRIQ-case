<template>
    <div class="bg-gray-100 min-h-screen p-6">
      <h1 class="text-4xl font-bold text-center mb-8 text-gray-900">Star Wars Characters</h1>
      <FilterControls :filters="filters" />
      <CharacterList :filteredCharacters="filteredCharacters" :loading="loading" />
      <Pagination 
        :filteredCharacters="filteredCharacters" 
        :characters="characters" 
        :totalCount="totalCount" 
        :loading="loading" 
        :nextPageUrl="nextPageUrl" 
        :fetchPage="fetchPage" 
        :fetchAllPages="fetchAllPages" 
      />
      <div v-if="loading" class="text-center mt-4">
        <span class="text-gray-700">Loading...</span>
      </div>
    </div>
</template>
  
<script setup>
  const filters = ref({
    male: false,
    female: false,
    birthYear: false
  });
  
  const characters = ref([]);
  const totalCount = ref(0); 
  const nextPageUrl = ref('https://swapi.dev/api/people');
  const loading = ref(false);
  
  const fetchData = async () => {
    try {
      const response = await fetch(nextPageUrl.value);
      const data = await response.json();
      characters.value.push(...data.results);
      totalCount.value = data.count;
      nextPageUrl.value = data.next;
    } catch (error) {
      console.error('Error fetching data:', error);
    }
  };
  
  const fetchPage = async () => {
    if (nextPageUrl.value && !loading.value) {
      loading.value = true;
      try {
        await fetchData();
      } finally {
        loading.value = false;
      }
    }
  };
  
  const fetchAllPages = async () => {
    if (!loading.value) {
      loading.value = true;
      try {
        while (nextPageUrl.value) {
          await fetchData();
        }
      } finally {
        loading.value = false;
      }
    }
  };
  
  const filteredCharacters = computed(() => {
    return characters.value.filter(character => {
      let pass = true;
      if (filters.value.male && character.gender !== 'male') pass = false;
      if (filters.value.female && character.gender !== 'female') pass = false;
      if (filters.value.birthYear) {
        const birthYear = character.birth_year.replace('BBY', '').trim();
        if (isNaN(birthYear) || birthYear < 20 || birthYear > 40) pass = false;
      }
      return pass;
    });
  });
  
  onMounted(fetchPage);
</script>
  