<template>
  <div class="search-container">
    <h1>Search and List Results</h1>
    <div class="search-bar">
      <input v-model="query" @keyup.enter="search" placeholder="Enter search term" />
      <button @click="search" class="search-button">Search</button>
    </div>
    <ul v-if="results.length">
      <li v-for="result in results" :key="result.id">
        <a :href="`${result.url}`" target="_blank">{{ result.title }}</a>
      </li>
    </ul>
    <p v-if="results.length === 0 && query !== ''">There were no results.</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      query: '',
      results: []
    };
  },
  methods: {
    async search() {
      const response = await fetch(`http://localhost:8080/search?query=${this.query}`);
      let data = await response.json();

     this.results = data.results; 

    }
  }
};
</script>

<style scoped>
.search-container {
  text-align: center;
  margin-top: 20px;
}

.search-bar {
  display: flex;
  justify-content: center;
  align-items: center;
  margin-bottom: 20px;
}

input {
  padding: 0.5rem;
  font-size: 1rem;
  margin-right: 0.5rem;
  border: 2px solid #ccc;
  border-radius: 5px;
  width: 300px;
}

.search-button {
  padding: 0.5rem 1rem;
  font-size: 1rem;
  border: none;
  border-radius: 5px;
  background-color: #007bff;
  color: white;
  cursor: pointer;
  transition: background-color 0.3s;
}

.search-button:hover {
  background-color: #0056b3;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  padding: 0.5rem;
  border-bottom: 1px solid #ccc;
}

a {
  color: #007bff;
  text-decoration: none;
  transition: color 0.3s;
}

a:hover {
  color: #0056b3;
}
</style>
