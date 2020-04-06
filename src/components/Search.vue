<template>
	<div class="search">
		<h1>Search images from NASA:</h1>
		<form v-on:submit.prevent="getResult(query)">
			<input type="text" v-model="query" />
		</form>
    <div class="images" v-if="results">
      <div v-for="(result, key) in results" :key="key">
        <img :src="result.links[0].href" />
      </div>
    </div>
	</div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'Search',
  data() {
    return {
      query: '',
      results: ''
    }
  }, 
  methods: {
    getResult(query) {
      axios.get('https://images-api.nasa.gov/search?media_type=image&q=' + query).then(response => {
        this.results = response.data.collection.items
      })
    }
  }
}
</script>
<style scoped>
.images img{
  height: 300px;
  margin: 10px;
} 
</style>