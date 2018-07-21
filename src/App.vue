<template>
  <div class="search">

<h2>Type in your Search</h2>

   <form v-on:submit.prevent="getResult(query)">
     <input type="text" placeholder="Type in your search" v-model="query" />
   </form>

    <div class="results" v-if="results">

      <div v-for="result in results">
        <img v-bind:src="result.links[0].href" />
      </div>
    </div>

  </div>
</template>

<script>
  import axios from 'axios';
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

    getResult(query) {
      axios.get('https://images-api.nasa.gov/search?q=' + query + '&media_type=image').then( response => {
        console.log(response.data.collection.items);
        this.results = response.data.collection.items;
        });
    }

  }
}
</script>

<style>
.search {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
