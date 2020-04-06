<template>
	<div class="search">
		<h1>Search images from NASA:</h1>
		<form v-on:submit.prevent="getResult(query)">
			<input type="text" v-model="query" />
		</form>
	</div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'Search',
  data() {
    return {
      query: '',
    }
  }, 
  methods: {
    getResult(query) {
      axios.get('https://images-api.nasa.gov/search?media_type=image&q=' + query).then(response => {
        console.log(response.data.collection.items)
      })
    }
  }
}
</script>