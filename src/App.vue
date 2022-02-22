<template>
	<h1>Morpion</h1>
	<div class="wrapper">
		<div class="text">
			<Infos
				@start="startGame"
				:isStarted="isStarted"
				:playerPlaying="playerPlaying"
			/>
		</div>
		<Grid
			@togglePlayer="togglePlayer"
			@end="endGame"
			:playerPlaying="playerPlaying"
		/>
	</div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import Infos from "./components/Infos.vue";
import Grid from "./components/Grid.vue";
export default defineComponent({
	data() {
		return {
			isStarted: false,
			playerPlaying: 1,
		};
	},
	components: { Infos, Grid },
	methods: {
		startGame() {
			this.isStarted = true;
		},
		togglePlayer() {
			if (this.playerPlaying === 1) {
				this.playerPlaying = 2;
			} else {
				this.playerPlaying = 1;
			}
		},
		endGame() {
			this.isStarted = false;
		},
	},
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
</style>
