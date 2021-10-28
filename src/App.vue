<template>
	<Navbar></Navbar>
	
	<div class="container">
		<div class="content">
			<div class="cards-grid">
				<div v-for="item in repos" :key="item.id">
					<Repocard :repository="item"></Repocard>
				</div>
			</div>
		</div>
	</div>
</template>

<script>
import Navbar from './components/Navbar.vue'
import Repocard from './components/Repocard.vue' 

export default {
	methods: {
		fetchData () {
			let date = this.createdBefore;
			let page = this.page;
			let API_Endpoint = `https://api.github.com/search/repositories?q=created:>${date}&sort=stars&order=desc&page=${page}`
			fetch(API_Endpoint)
				.then(res => res.json())
				.then(result => {
					console.log('Result fetch data : ', result);
					this.repos = result.items;
				})
		},
	},
	data () {
		return {
			createdBefore: (() => {
				var date = new Date(new Date().getFullYear(), new Date().getMonth() - 1, new Date().getDate());
				return date.toISOString().split('T')[0];
			})(),
			page: 1,
			API_Endpoint: `https://api.github.com/search/repositories?q=created:>${this.createdBefore}&sort=stars&order=desc&page=${this.page}`,
			repos: null,
			created_after: null,
		}
	},
	name: "App",
	components: {
		Navbar, Repocard
	},
	mounted() {
		this.fetchData();
	}
}
</script>

<style lang="less">
// I Always reset everything so i have controle over everything 😈.
*{
	margin: 0px;
	padding: 0px;
	box-sizing: border-box;
	font-family: 'Montserrat', sans-serif;
}

.container{
	height: 100vh;
	width: 100vw;
	overflow-y: auto;
	overflow-x: hidden;
	scroll-behavior: smooth;
	background: black;
	color: white;
	display: flex;
	justify-content: center;
}

.content{
	margin-top:80px;
	margin-bottom: 50px;
	color: white;
	width: 90vw;
	max-width: 1600px;
}

.cards-grid{
	display: flex;
	flex-direction: column;
	gap: 20px;
}
</style>
