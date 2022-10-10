<script lang="ts">
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://v3.vuejs.org/api/sfc-script-setup.html#sfc-script-setup

import axios from './middleware'
import { computed, defineComponent, ref } from 'vue'

export default defineComponent({
  setup() {
    const searchTerm = ref('')
    const searchResults = ref([])

    const endpoint = computed(() =>
      searchTerm.value.length ? '/breeds/search' : '/breeds'
    )

    async function runSearch() {
      const response = await axios.get(endpoint.value, {
        params: {
          q: searchTerm.value,
          limit: 20,
        },
      })

      searchResults.value = response.data
    }

    return { searchTerm, searchResults, runSearch }
  },
})
</script>

<template>
  <main>
    <input type="text" class="text" v-model="searchTerm" />
    <button @click="runSearch">Search</button>
    {{ searchTerm }}
    <ul>
      <li v-for="result in searchResults" :key="result.id">
        {{ result.name }}
      </li>
    </ul>
  </main>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
ul {
  list-style-type: none;
}
</style>
