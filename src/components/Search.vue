<template>
  <div class="search">
    <h2>Type your favorite food</h2>
    <form v-on:submit.prevent="getResult(query)">
      <input type="text" placeholder="Type your favorite food" v-model="query"> <br>
      <button @click="getResult"> Search </button><br>
    </form><br>
    <div class="results" v-if="results">

      <div v-for="result in results" :key="result.id">
        <img width="250px" v-bind:src="result.strMealThumb" />
        <h1 v-bind:title="result.strMeal"></h1>
        <p v-bind:caption="result.strTags"></p>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'search',
  data () {
    return {
      msg: 'Search',
      query: '',
      results: ''
    }
  },
  methods: {
    getResult (query) {
      axios.get('https://www.themealdb.com/api/json/v1/1/search.php?s=' + query).then(response => {
        console.log(response.data.meals)
        this.results = response.data.meals
      })
    }
  }
}
</script>

<style scoped>
.result img {
  height: 300px;
  margin: 10px;
}

h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}

input {
    width: 40%;
    padding: 12px 20px;
    margin: 8px 0;
    display: inline-block;
    border: 1px solid #ccc;
    border-radius: 4px;
    box-sizing: border-box;
  }

button {
    background-color: #4CAF50;
    border: none;
    color: white;
    padding: 15px 32px;
    text-align: center;
    text-decoration: none;
    display: inline-block;
    font-size: 16px;
  }


</style>
