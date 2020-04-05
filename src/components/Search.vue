<template>
	<div class="search">
		<h1>{{ msg }}</h1>
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
      msg: "Search",
      query: "This is a query string"
    }
  }, 
  methods: {
    getResult() {
      axios.get('http://www.reddit.com/r/pics.json').then(response => {
        alert(response.data)
      })
    }
  }
}
</script>
