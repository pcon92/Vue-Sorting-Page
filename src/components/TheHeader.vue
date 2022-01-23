<template>
	<div id="outer-container">
		<div class="card-options" id="top-options">
			<p class="caption">Available:</p>
			<li
				v-for="card in cards"
				:class="getAllCardsClass(card.name)"
				:key="card.id"
				@click="addCard(card.name)"
			>
				{{ card.name }} Sort
			</li>
		</div>
		<div class="card-options" id="bottom-options">
			<p class="caption">Selected:</p>
			<li
				v-for="card in activeCards"
				class="card-div selected"
				:key="card.id"
				@click="removeCard(card.name)"
			>
				{{ card.name }} Sort
			</li>
		</div>
	</div>
</template>

<script>
export default {
	props: {
		cards: {
			type: Array,
			required: true,
		},
		activeCards: {
			type: Array,
			required: true,
		},
	},
	emits: ["add-card", "remove-card"],
	data() {
		return {};
	},
	methods: {
		addCard(name) {
			if (!this.checkIfActive(name)) {
				this.$emit("add-card", name);
			}
		},
		removeCard(name) {
			if (this.checkIfActive(name)) {
				this.$emit("remove-card", name);
			}
		},
		checkIfActive(name) {
			const filteredCards = this.activeCards.filter(
				(card) => card.name === name
			);
			return filteredCards.length;
		},
		getAllCardsClass(name) {
			if (this.checkIfActive(name)) {
				return "card-div unselected-disabled";
			} else {
				return "card-div unselected-active";
			}
		},
	},
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#outer-container {
	height: 100%;
	display: flex;
	flex-direction: column;
	justify-content: space-between;
	background-color: var(--background-for-header-area);
	color: var(--white);
}
.caption {
	width: 150px;
	font-weight: bold;
	margin-left: 1%;
	display: flex;
	align-items: center;
	color: var(--font-color-header-caption);
}
.card-options {
	display: flex;
}
#top-options {
	height: 35%;
}
#bottom-options {
	height: 55%;
}
.card-div {
	width: 100%;
	display: flex;
	justify-content: center;
	align-items: center;
}
.unselected-active {
	border: 1px solid var(--light-grey);
	border-radius: 5px;
	animation: unselectedActiveMove 3s infinite;
}
.unselected-disabled {
	border: 1px solid var(--light-grey);
	border-radius: 5px;
	opacity: 0.35;
}
.selected {
	border: 1px solid var(--light-grey);
	border-radius: 5px;
}

/* Animations */
@keyframes unselectedActiveMove {
	0% {
		transform: translateY(0px);
	}
	40% {
		transform: translateY(3px);
	}

	60% {
		transform: translateY(3px);
	}

	100% {
		transform: translateY(0px);
	}
}

/* Media queries */

@media (max-width: 20rem) {
	/* 320 pixels */
	.caption {
		width: 60px;
		font-size: 0.7rem;
		margin-right: 10px;
	}
	.card-div {
		width: 55px;
		font-size: 0.7rem;
		text-align: center;
	}
}

@media (min-width: 20rem) {
	/* 320 pixels */
	.caption {
		width: 60px;
		font-size: 0.7rem;
		margin-right: 10px;
	}
	.card-div {
		font-size: 0.7rem;
	}
}

@media (min-width: 40rem) {
	/* 640 pixels */
	.caption {
		width: 100px;
		font-size: 1rem;
	}
	.card-div {
		font-size: 1rem;
	}
}

@media (min-width: 60rem) {
	/* 960 pixels */
	.unselected-active:hover {
		background-color: var(--vue-orange);
		cursor: pointer;
	}
	.unselected-disabled:hover {
		cursor: not-allowed;
	}
	.selected:hover {
		background-color: var(--vue-red);
		cursor: pointer;
	}
}
</style>
