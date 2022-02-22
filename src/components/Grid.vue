<template>
	<div class="grid">
		<div v-if="!isStarted" class="disableGrid"></div>
		<Cell
			@updateGame="updateGame"
			v-for="cellUnit in gridSize"
			:key="cellUnit"
			:id="cellUnit"
			:isStarted="isStarted"
			:playerPlaying="playerPlaying"
			ref="cell"
		/>
	</div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import Cell from "./Cell.vue";

interface CellImgAndId {
	id: number;
	img: string;
}

export default defineComponent({
	props: {
		playerPlaying: {
			type: Number,
			required: true,
		},
		isStarted: {
			type: Boolean,
			required: true,
		},
	},
	emits: ["end", "updateGame"],
	data() {
		return {
			gridSize: 9,
			clicked: false,
			gridContent: [] as string[],
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
			winner: 0,
		};
	},
	components: { Cell },
	watch: {
		isStarted(newVal: boolean) {
			if (newVal === true) {
				this.gridContent = [];
			}
		},
	},
	methods: {
		updateGame(cellImgAndId: CellImgAndId) {
			this.gridContent[cellImgAndId.id] = cellImgAndId.img;
			this.checkWinner();
		},
		checkWinner() {
			this.wins.map((el) => {
				const val1 = this.gridContent[el[0]];
				const val2 = this.gridContent[el[1]];
				const val3 = this.gridContent[el[2]];

				if (val1 !== undefined && val2 !== undefined && val3 !== undefined) {
					if (val1 === val2 && val2 === val3) {
						this.$emit("end", this.playerPlaying);
						return;
					}
				}
			});
			this.$emit("updateGame");
		},
	},
});
</script>

<style scoped>
.grid {
	width: 40vw;
	max-width: 40vw;
	max-height: 40vw;
	padding: 3vw;
	display: flex;
	flex-wrap: wrap;
	position: relative;
}
.disableGrid {
	position: absolute;
	width: 100%;
	height: 100%;
	background-color: rgba(255, 255, 255, 0.24);
	z-index: 1;
}
</style>
