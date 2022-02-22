<template>
	<h1>Morpion</h1>
	<div class="wrapper">
		<div class="text">
			<Infos
				@start="startGame"
				:isStarted="isStarted"
				:playerPlaying="playerPlaying"
				:winner="winner"
				:lost="lost"
			/>
		</div>
		<Grid
			@updateGame="updateGame"
			@end="endGame"
			:isStarted="isStarted"
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
			lapsRemaining: 9,
			winner: 0,
			lost: false,
		};
	},
	components: { Infos, Grid },
	watch: {
		lapsRemaining(newValue: number) {
			if (newValue === 0) {
				if (this.winner === 0) {
					this.lost = true;
				}
				this.endGame();
			}
		},
	},
	methods: {
		startGame() {
			this.winner = 0;
			this.lost = false;
			this.playerPlaying = 1;
			this.lapsRemaining = 9;
			this.isStarted = true;
		},
		updateGame() {
			if (this.playerPlaying === 1) {
				this.playerPlaying = 2;
			} else {
				this.playerPlaying = 1;
			}
			this.lapsRemaining--;
		},
		endGame(winner: number = 0) {
			this.winner = winner;
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
