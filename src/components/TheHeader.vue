<template>
	<div id="outer-container">
		<div class="card-options" id="top-options">
			<p class="caption" id="top-caption">Choose from:</p>
			<li
				v-for="card in cards"
				:class="getAllCardsClass(card.name)"
				:key="card.id"
				@click="selectCard(card.name)"
			>
				{{ card.name }} Sort
			</li>
		</div>
		<div class="card-options" id="bottom-options">
			<p class="caption" id="bottom-caption">Chosen cards:</p>
			<li
				v-for="card in selectedCards"
				class="card-div selected"
				:key="card.id"
				@click="removeCard(card)"
			>
				{{ card }} Sort
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
	},
	emits: ["add-card", "remove-card"],
	data() {
		return {
			selectedCards: [],
		};
	},
	methods: {
		selectCard(name) {
			if (!this.checkIfActive(name)) {
				this.selectedCards.push(name);
				this.$emit("add-card", name);
			}
		},
		removeCard(name) {
			if (this.checkIfActive(name)) {
				const filteredCards = this.selectedCards.filter(
					(card) => card !== name
				);
				this.selectedCards = filteredCards;
				this.$emit("remove-card", name);
			}
		},
		checkIfActive(name) {
			const filteredCards = this.selectedCards.filter(
				(card) => card === name
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
	created() {
		const defaultCards = this.cards.find((card) => card.isShown === true);
		this.selectedCards.push(defaultCards.name);
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
	width: 200px;
	display: flex;
	justify-content: center;
	align-items: center;
}
.unselected-active {
	border: 1px solid var(--light-grey);
	border-radius: 5px;
}
.unselected-disabled {
	border: 1px solid var(--light-grey);
	border-radius: 5px;
	opacity: 0.35;
}
.unselected-active:hover {
	background-color: var(--vue-orange);
	cursor: pointer;
}
.unselected-disabled:hover {
	cursor: not-allowed;
}
.selected {
	border: 1px solid var(--light-grey);
	border-radius: 5px;
}
.selected:hover {
	background-color: var(--vue-red);
	cursor: pointer;
}
</style>
