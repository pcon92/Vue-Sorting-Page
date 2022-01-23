<template>
	<div id="header-div">
		<the-header
			:cards="algorithms"
			:activeCards="activeCards"
			@add-card="addCard"
			@remove-card="removeCard"
		></the-header>
	</div>
	<div id="card-area-div">
		<transition-group name="card-transition" appear>
			<sorting-card
				v-for="activeCard in activeCards"
				:key="activeCard.id"
				:starting-numbers="startingNumbers"
				:active-card="activeCard.name"
				:bullet-points="activeCard.bulletPoints"
				:is-shown="activeCard.isShown"
				class="sorting-card-component"
				@remove-card="removeCard"
			/>
		</transition-group>
	</div>
	<div id="footer-div">
		<the-footer :name="name" :year="year" :links="links"></the-footer>
	</div>
</template>

<script>
import theHeader from "./components/TheHeader.vue";
import sortingCard from "./components/SortingCard.vue";
import theFooter from "./components/TheFooter.vue";

export default {
	name: "App",
	components: {
		theHeader,
		sortingCard,
		theFooter,
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
						"Steps through array starting from left",
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
				{
					name: "Selection",
					bulletPoints: [
						"Divide into sorted and unsorted partitions",
						"Find smallest value in unsorted",
						"Move that value to the front of sorted",
					],
					isShown: false,
					id: 3,
				},
				{
					name: "Shell",
					bulletPoints: [
						"A variation of insertion sort",
						"Using Shell's original sequence as intervals",
						"Compare elements at interval to swap",
					],
					isShown: false,
					id: 4,
				},
			],
			activeCards: [],
			name: "Paul C",
			year: "2022",
			links: [
				{
					name: "Github",
					url: "https://github.com/pcon92",
					icon: "fab fa-github fa-2x",
					id: 0,
				},
				{
					name: "Portfolio",
					url: "https://paulc-portfolio.netlify.app/",
					icon: "far fa-folder fa-2x",
					id: 1,
				},
				{
					name: "Email",
					url: "mailto:palu_comgui@outlook.com",
					icon: "far fa-envelope fa-2x",
					id: 2,
				},
			],
		};
	},
	methods: {
		addCard(name) {
			const pickedCard = this.algorithms.find(
				(algorithm) => algorithm.name === name
			);
			this.activeCards.push(pickedCard);
			console.log("e");
		},
		removeCard(name) {
			const filteredCards = this.activeCards.filter(
				(algorithm) => algorithm.name !== name
			);
			this.activeCards = filteredCards;
			console.log("e");
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

	/* Fixes issues on mobile compared to vh/vw with scroll */
	position: fixed;
	top: 0;
	bottom: 0;
	left: 0;
	right: 0;
}
#header-div {
	height: 10%;
}
#card-area-div {
	overflow: auto;
	width: 100%;
	display: flex;
	flex-direction: column;
	align-items: center;
	height: 85%;
	background-color: var(--background-for-card-area);
}
#footer-div {
	height: 5%;
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

/* Media queries */

@media (max-width: 20rem) {
	/* 320 pixels */
	.sorting-card-component {
		margin: 10px 20px 10px 20px;
	}
}

@media (min-width: 20rem) {
	/* 320 pixels */
	.sorting-card-component {
		margin: 15px 25px 15px 25px;
	}
}

@media (min-width: 40rem) {
	/* 640 pixels */
	.sorting-card-component {
		margin: 25px;
	}
}

@media (min-width: 60rem) {
	/* 960 pixels */
}
</style>
