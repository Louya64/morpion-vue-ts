<template>
	<div class="cell" @click="displayImg">
		<h2>cell {{ id }}</h2>
		<img class="invisible" ref="img" :src="imgUrl" alt="alt" />
	</div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import "../assets/circle.svg";

export default defineComponent({
	props: {
		id: {
			type: Number,
			required: true,
		},
		playerPlaying: {
			type: Number,
			required: true,
		},
		isStarted: {
			type: Boolean,
			required: true,
		},
	},
	data() {
		return {
			imgUrl: "src/assets/circle.svg",
			filled: false,
		};
	},
	$refs: {
		img: HTMLElement,
	},
	watch: {
		isStarted(newVal) {
			if (newVal === true) {
				const img: HTMLElement = this.$refs.img as HTMLElement;
				img.classList.add("invisible");
				this.filled = false;
			}
		},
	},
	methods: {
		displayImg() {
			if (!this.filled) {
				if (this.playerPlaying === 1) {
					this.imgUrl = "src/assets/cross.svg";
				} else {
					this.imgUrl = "src/assets/circle.svg";
				}
				const img: HTMLElement = this.$refs.img as HTMLElement;
				img.classList.remove("invisible");
				this.filled = true;
				this.$emit("updateGame", { id: this.id, img: this.imgUrl });
			}
		},
	},
});
</script>

<style scoped>
.cell {
	margin: 0;
	width: 10vw;
	height: 10vw;
	background-color: blueviolet;
	border: 1px solid #fff;
}
.invisible {
	display: none;
}
</style>
