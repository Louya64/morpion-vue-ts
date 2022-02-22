<template>
	<div class="cell" @click.once="displayImg">
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
	},
	data() {
		return {
			imgUrl: "src/assets/circle.svg",
		};
	},
	$refs: {
		img: HTMLImageElement,
	},
	methods: {
		displayImg() {
			if (this.playerPlaying === 1) {
				this.imgUrl = "src/assets/cross.svg";
			} else {
				this.imgUrl = "src/assets/circle.svg";
			}
			const img: HTMLImageElement = this.$refs.img as HTMLImageElement; // ??????????????????????????????????
			console.log(this.id, this.imgUrl);
			img.classList.remove("invisible");
		},
	},
});
</script>

<style>
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
