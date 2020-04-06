<template>
	<div class="search">
		<form v-on:submit.prevent="getResult(query)">
			<input type="text" v-model="query" />
		</form>
		<section v-if="error">
			<p>There has been an error: {{ error }}</p>
		</section>  
		<section v-else>
      <Gallery :results="results"></Gallery>
    </section>
	</div>
</template>

<script>
import axios from "axios";
import Gallery from "@/components/Gallery";

export default {
  name: 'Search',
  components: {
    Gallery
  },
	data() {
		return {
      query: '',
      results: [],  
			error: false
		};
	},
	methods: {
		getResult(query) {
      this.results = []
			axios
				.get('https://images-api.nasa.gov/search?media_type=image&q=' + query)
				.then(response => {
          this.results = response.data.collection.items;
				})
				.catch(error => {
          console.log(error)
        })  
        .finally(() => { alert(this.results.length + ' result(s) found') })
		}
  }
};
</script>
<style scoped scss>
.search {
	text-align: center;
}
.search input {
	padding: 6px;
	margin-bottom: 12px;
	font-size: 18px;
}
</style>