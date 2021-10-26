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
	data () {
		return {
			repos: null
		}
	},
	name: "App",
	components: {
		Navbar, Repocard
	},
	mounted () {
		fetch("https://api.github.com/search/repositories?q=created:>2017-10-22&sort=stars&order=desc&page=1")
			.then(res => res.json())
			.then(result => {
				console.log('Result fetch data : ', result);
				this.repos = result.items;
			})
	}
}
</script>

<style lang="less">
// I Always reset everything so i have controle over everything 😈
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
