<template>
	<div id="app">
		<main>
			<h2 class="title">Ты сегодня покормил кота?</h2>
			<div class="card-list">
				<Card v-for="(food, id) in foods" :key="id" :card_id="id" :card="food" />
			</div>
		</main>
	</div>
</template>

<script>
import Card from "./components/Card.vue";

export default {
	name: "App",
	components: {
		Card,
	},
	data() {
		return {
			foods: [
				{
					taste: "с фуа-гра",
					servings: "10",
					gift: "1",
					weight: "0,5",
					description: "Печень утки разварная с артишоками.",
				},
				{
					taste: "с рыбой",
					servings: "40",
					gift: "2",
					weight: "2",
					description: "Головы щучьи с чесноком да свежайшая сёмгушка.",
				},
				{
					taste: "с курой",
					servings: "100",
					gift: "5",
					weight: "5",
					description: "Филе из цыплят с трюфелями в бульоне.",
					is_ended: true,
				},
			],
		};
	},
};
</script>

<style lang="scss">
@import url("~@/assets/fonts/TrebuchetMS/stylesheet.css");
@import url("~@/assets/fonts/Exo20-Thin/stylesheet.css");

html,
body {
	margin: 0;
	padding: 0;
	border: 0;
	height: 100%;
	min-height: 100%;
	position: relative;
}
body {
	text-align: center;
	font-family: "Trebuchet MS";
	background-image: url("./assets/bg-fon.png");
}

#app {
	position: absolute;
	top: 0;
	left: 0;
	height: 100%;
	min-width: 100%;
}

main {
	min-height: 100vh;
	background-image: linear-gradient(
		180deg,
		rgba(0, 0, 0, 0.5) 0%,
		rgba(0, 0, 0, 0) 50%,
		rgba(0, 0, 0, 0.5) 100%
	);
	display: flex;
	flex-direction: column;
	justify-content: center;
}

p {
	color: #666;
}

.title {
	color: #fff;
	font-family: "Exo 2.0 Thin";
	font-weight: 100;
	font-size: 36px;
}

.card-list {
	display: flex;
	justify-content: space-around;
	align-items: center;
}

.card-item {
	width: 28%;
}

@media screen and (max-width: 1030px) {
	.card-list {
		flex-wrap: wrap;
	}
	.card-item {
		width: 40%;
		margin: 10px 10px;
	}
}

@media screen and (max-width: 752px) {
	.card-list {
		flex-direction: column;
		align-items: center;
	}
	.card-item {
		width: 50%;
	}
}
</style>
