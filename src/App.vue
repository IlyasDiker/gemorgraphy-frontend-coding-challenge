<template>
	<Navbar @selectedMode="onModeChange"></Navbar>
	
	<div class="container">
		<div class="content">
			<div class="cards-grid">
				<template v-if="repos.length > 0" >
					<div v-for="item in repos" :key="item.id">
						<Repocard :repository="item"></Repocard>
					</div>
					<div class="pagination-wrapper" v-if="paginationMode == 'PAGES'">
						<ul>
							<li v-for="n in 10" :key="n">
								<!-- Let's have 10 pages just for the test -->
								<button 
									:class="{active: page == n}"
									v-on:click="goToPage(n)"
									>{{n}}</button>
							</li>
						</ul>
					</div>
					<div class="pagination-wrapper" v-if="paginationMode == 'LOAD_MORE'">
						<button
							v-on:click="loadMore()"
							:disabled="page >= pages_count"
							>Load More</button>
					</div>
				</template>
				<div class="loading" v-else>
					<i class='bx bx-loader-alt bx-spin'></i>
				</div>
			</div>
		</div>
		<div class="loading-page" v-if="isPageLoading">
			<i class='bx bx-loader-alt bx-spin'></i>
		</div>
	</div>
</template>

<script>
import Navbar from './components/Navbar.vue'
import Repocard from './components/Repocard.vue' 
import { ObserveVisibility } from "vue-observe-visibility";

export default {
	directives: {
		ObserveVisibility
	},
	methods: {
		onModeChange (mode) {
			this.paginationMode = mode;
		},
		gotoTop () {
			document.querySelector('.container').scrollTo(0,0)
		},
		goToPage (index) {
			this.page = index;
			this.fetchData({append: false});
			this.gotoTop();
		},
		loadMore () {
			if (this.page < this.pages_count) {
				this.page++;
				this.fetchData({append: true});
			}
		},
		fetchData (req = {append: false}) {
			let date = this.createdBefore;
			let page = this.page;
			let API_Endpoint = `https://api.github.com/search/repositories?q=created:>${date}&sort=stars&order=desc&page=${page}`
			fetch(API_Endpoint)
				.then(res => res.json())
				.then(result => {
					console.log('Result fetch data : ', result);
					if(result.total_count){
						this.pages_count = Math.ceil(result.total_count / result.items.length);
						console.log(this.pages_count);
					}
					if(result.items){
						if(req.append){
							result.items.forEach(element => {
								this.repos.push(element);
							});
						} else {
							this.repos = result.items;
						}
					}
				})
		}
	},
	data () {
		return {
			createdBefore: (() => {
				var date = new Date(new Date().getFullYear(), new Date().getMonth() - 1, new Date().getDate());
				return date.toISOString().split('T')[0];
			})(),
			page: 1,
			pages_count: 0,
			repos: [],
			created_after: null,
			paginationMode: 'LOAD_MORE',
			isPageLoading: false,
		}
	},
	name: "App",
	components: {
		Navbar, Repocard
	},
	mounted() {
		this.fetchData({append: false});
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
	margin-top:100px;
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

.loading{
	padding: 10px;
	text-align: center;
}

.pagination-wrapper{
	display: flex;
	justify-content: center;
	margin: 20px 0 20px 20px;
	ul{
		list-style: none;
		display: flex;
		flex-direction: row;
		gap: 10px;
	}
}

</style>
