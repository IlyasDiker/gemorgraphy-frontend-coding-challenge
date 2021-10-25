<template>
	<Navbar></Navbar>
	<div class="container">
		<div class="content">
			<h1>tedsasd</h1>
		</div>
	</div>
</template>

<script>
import Navbar from './components/Navbar.vue'

export default {
	name: "App",
	components: {
		Navbar

	},
};
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
	background: black;
	color: white;
}

.content{
	margin-top:80px;
	color: white;
}
</style>
