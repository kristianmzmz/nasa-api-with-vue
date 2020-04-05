<template>
	<div class="search">
		<h1>{{ msg }}</h1>
		<form v-on:submit.prevent="getResult(query)">
			<input type="text" v-model="query" />
		</form>
	</div>
</template>

<script>
export default {
  name: 'Search',
  data() {
    return {
      msg: "Search",
      query: "This is a query string"
    }
  }, 
  methods: {
    getResult(query) {
      alert(query);
    }
  }
}
</script>
