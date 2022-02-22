<template>
	<div class="grid">
		<Cell
			@click.once="updateGame"
			v-for="cellUnit in gridSize"
			:key="cellUnit"
			:id="cellUnit"
			:playerPlaying="playerPlaying"
		/>
	</div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import Cell from "./Cell.vue";

export default defineComponent({
	props: {
		playerPlaying: {
			type: Number,
			required: true,
		},
	},
	data() {
		return {
			gridSize: 9,
			lapsRemaining: 9,
			wins: [
				[1, 2, 3],
				[4, 5, 6],
				[7, 8, 9],
				[1, 4, 7],
				[2, 5, 8],
				[3, 6, 9],
				[1, 5, 9],
				[7, 5, 3],
			],
		};
	},
	components: { Cell },
	watch: {
		lapsRemaining(newValue) {
			console.log(newValue);
			if (newValue === 0) {
				this.$emit("end");
			}
		},
	},
	methods: {
		updateGame() {
			this.lapsRemaining--;
			this.$emit("togglePlayer");
		},
	},
});
</script>

<style>
.grid {
	max-width: 40vw;
	max-height: 40vw;
	padding: 3vw;
	display: flex;
	flex-wrap: wrap;
}
</style>
