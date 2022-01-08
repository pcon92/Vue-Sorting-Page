<template>
	<bubble-sort :startingNumbers="startingNumbers"></bubble-sort>
</template>

<script>
import BubbleSort from "./components/BubbleSort.vue";

export default {
	name: "App",
	components: {
		BubbleSort,
	},
	data() {
		return {
			startingNumbers: [
				{ value: 4, id: Math.random() * 999 },
				{ value: 2, id: Math.random() * 999 },
				{ value: 6, id: Math.random() * 999 },
				{ value: 8, id: Math.random() * 999 },
				{ value: 2, id: Math.random() * 999 },
				{ value: 9, id: Math.random() * 999 },
				{ value: 1, id: Math.random() * 999 },
				{ value: 3, id: Math.random() * 999 },
			],
		};
	},
	methods: {},
};
</script>

<style>
#app {
	font-family: Avenir, Helvetica, Arial, sans-serif;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
	display: flex;
	justify-content: center;
	align-items: center;
}
</style>
