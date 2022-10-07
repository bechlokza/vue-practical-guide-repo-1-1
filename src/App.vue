<script>
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://v3.vuejs.org/api/sfc-script-setup.html#sfc-script-setup

import axios from './middleware'

export default {
  data() {
    return {
      searchTerm: '',
      searchResults: [],
    }
  },
  computed: {
    endpoint() {
      return this.searchTerm.length ? '/breeds/search' : '/breeds'
    },
  },
  methods: {
    async runSearch() {
      const response = await axios.get(this.endpoint, {
        q: this.searchTerm,
      })

      this.searchResults = response.data
    },
  },
}
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
