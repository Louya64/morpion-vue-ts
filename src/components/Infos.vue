<template>
	<div class="infos">
		<button v-if="!isStarted" @click="start">Lancer la partie</button>
		<div v-if="isStarted">
			<p>Tour du joueur {{ playerPlaying }}</p>
		</div>
		<div>
			<p>score joueur 1 : {{ score1 }} points</p>
			<p>score joueur 2 : {{ score2 }} points</p>
		</div>
	</div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
export default defineComponent({
	props: {
		isStarted: {
			type: Boolean,
			required: true,
		},
		playerPlaying: {
			type: Number,
			required: true,
		},
	},
	data() {
		return {
			score1: 0,
			score2: 0,
		};
	},
	methods: {
		start() {
			this.$emit("start");
		},
	},
});
</script>

<style>
.infos {
	width: 20vw;
	border: 2px solid black;
	margin-top: 3vw;
}
</style>
