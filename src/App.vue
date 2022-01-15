<template>
	<the-header
		:cards="algorithms"
		@add-card="addCard"
		@remove-card="removeCard"
	></the-header>
	<transition-group name="card-transition" appear>
		<sorting-card
			v-for="activeCard in activeCards"
			:key="activeCard.id"
			:starting-numbers="startingNumbers"
			:active-card="activeCard.name"
			:bullet-points="activeCard.bulletPoints"
			:is-shown="activeCard.isShown"
			class="sorting-card-component"
		/>
	</transition-group>
</template>

<script>
import theHeader from "./components/TheHeader.vue";
import sortingCard from "./components/SortingCard.vue";

export default {
	name: "App",
	components: {
		theHeader,
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
					id: 1,
				},
				{
					name: "Insertion",
					bulletPoints: [
						"Starting from left of array",
						"Create sorted and unsorted partitions",
						"Sort next item into sorted partition",
					],
					isShown: false,
					id: 2,
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
	width: 100vw;
	overflow: hidden;
}
.sorting-card-component {
	margin: 25px;
}
.card-transition-enter-from {
	transform: translateX(-500px);
	opacity: 0;
}
.card-transition-enter-active,
.card-transition-leave-active {
	transition: all 0.25s ease;
}
.card-transition-leave-to {
	transform: translateX(500px);
	opacity: 0;
}
.card-transition-move {
	transition: all 0.25s linear;
}
</style>
