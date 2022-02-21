<template>
	<h1>titre</h1>
	<div class="wrapper">
		<div class="text">
			<!-- component infos -->
			<Text />
			<!-- <button>Jouer</button>
			<p>Tour de : {{ playerPlaying }}</p>
			<p>score j1, j2</p> -->
		</div>
		<div class="grid">
			<Grid />
			<!-- component grille de jeu -->
		</div>
	</div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import Text from "./components/text.vue";
import Grid from "./components/Grid.vue";
export default defineComponent({
	data() {
		return {
			playerPlaying: 1,
		};
	},
	components: { Text, Grid },
});
</script>

<style>
@import "./assets/base.css";

#app {
	max-width: 1280px;
	margin: 0 auto;
	padding: 2rem;
	text-align: center;
	font-weight: normal;
}
.wrapper {
	display: flex;
	margin: auto;
	justify-content: space-evenly;
}
.text,
.grid {
	width: 30vw;
	border: 2px solid black;
}
</style>
