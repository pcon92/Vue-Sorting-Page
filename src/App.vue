<template>
	<sorting-header
		:cards="algorithms"
		@add-card="addCard"
		@remove-card="removeCard"
	></sorting-header>
	<div v-for="(activeCard, index) in activeCards" :key="index">
		<sorting-card
			class="sorting-card-component"
			:startingNumbers="startingNumbers"
			:activeCard="activeCard.name"
			:bulletPoints="activeCard.bulletPoints"
			:isShown="activeCard.isShown"
		/>
	</div>
</template>

<script>
import sortingHeader from "./components/SortingHeader.vue";
import sortingCard from "./components/SortingCard.vue";

export default {
	name: "App",
	components: {
		sortingHeader,
		sortingCard,
	},
	data() {
		return {
			startingNumbers: [
				{ value: 4, id: Math.random() * 999, isFocused: false },
				{ value: 2, id: Math.random() * 999, isFocused: false },
				{ value: 6, id: Math.random() * 999, isFocused: false },
				{ value: 8, id: Math.random() * 999, isFocused: false },
				{ value: 2, id: Math.random() * 999, isFocused: false },
				{ value: 9, id: Math.random() * 999, isFocused: false },
				{ value: 1, id: Math.random() * 999, isFocused: false },
				{ value: 3, id: Math.random() * 999, isFocused: false },
			],
			algorithms: [
				{
					name: "Bubble",
					bulletPoints: [
						"Steps through list",
						"Compares adjacent elements",
						"Swaps them if they are in wrong order",
					],
					isShown: true,
				},
				{
					name: "Insertion",
					bulletPoints: [
						"Starting from left of array",
						"Create sorted and unsorted partitions",
						"Sort next item into sorted partition",
					],
					isShown: false,
				},
			],
			activeCards: [],
		};
	},
	methods: {
		addCard(name) {
			const pickedCard = this.algorithms.find(
				(algorithm) => algorithm.name === name
			);
			this.activeCards.push(pickedCard);
		},
		removeCard(name) {
			const filteredCards = this.activeCards.filter(
				(algorithm) => algorithm.name !== name
			);
			this.activeCards = filteredCards;
		},
	},
	created() {
		const defaultCards = this.algorithms.find(
			(card) => card.isShown === true
		);
		this.activeCards.push(defaultCards);
	},
};
</script>

<style>
#app {
	font-family: Avenir, Helvetica, Arial, sans-serif;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
	display: flex;
	flex-direction: column;
	justify-content: center;
	align-items: center;
	height: 100vh;
}
.sorting-card-component {
	margin: 25px;
}
</style>
