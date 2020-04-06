<template>
	<div class="search">
		<form v-on:submit.prevent="getResult(query)">
			<input type="text" v-model="query" />
		</form>
		<section v-if="error">
			<p>There has been an error: {{ error }}</p>
		</section>
		<section v-else>
      <div class="gallery cf" v-if="results.length != 0">
        <div v-if="loading">Loading...</div>
        <div 
          v-else 
          v-for="(result, key) in results" 
          :key="key">
            <img :src="result.links[0].href" />
        </div>
      </div>
    </section>
	</div>
</template>

<script>
import axios from "axios";

export default {
	name: 'Search',
	data() {
		return {
			query: '',
			results: '',
			loading: true,
			error: false
		};
	},
	methods: {
		getResult(query) {
			axios
				.get('https://images-api.nasa.gov/search?media_type=image&q=' + query)
				.then(response => {
					this.results = response.data.collection.items;
				})
				.catch(error => {
          console.log(error)
        })  
        .finally(() => {
          this.loading = false
        })
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

.gallery {
	width: 640px;
	margin: 0 auto;
	padding: 5px;
	background: #fff;
	box-shadow: 0 1px 1px rgba(0, 0, 0, 0.1);
}

.gallery > div {
	position: relative;
	float: left;
	padding: 5px;
	min-height: 220px;
}

.gallery > div > img {
	width: 200px;
	vertical-align: middle;
	transition: 0.1s transform;
	transform: translateZ(0); /* hack */
}

.gallery > div:hover {
	z-index: 1;
}

.gallery > div:hover > img {
	transform: scale(1.8, 1.8);
	transition: 0.3s transform;
}

.cf:before,
.cf:after {
	display: table;
	content: "";
	line-height: 0;
}

.cf:after {
	clear: both;
}
</style>