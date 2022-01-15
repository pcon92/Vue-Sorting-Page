<template>
	<div id="outer-container">
		<div id="all-cards">
			<li
				v-for="(card, index) in cards"
				class="card-div unselected"
				:key="index"
			>
				{{ card.name }} Sort
				<div
					class="change-cards-btn add-card"
					@click="selectCard(card.name)"
					:disabled="false"
				>
					<div v-if="!checkIfActive(card.name)">+</div>
				</div>
			</li>
		</div>
		<div id="selected-cards">
			<li
				v-for="(card, index) in selectedCards"
				class="card-div selected"
				:key="index"
			>
				{{ card }} Sort
				<div
					class="change-cards-btn remove-card"
					@click="removeCard(card)"
				>
					X
				</div>
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
		return {
			selectedCards: [],
		};
	},
	methods: {
		selectCard(name) {
			this.selectedCards.push(name);
			this.$emit("add-card", name);
		},
		removeCard(name) {
			const filteredCards = this.selectedCards.filter(
				(card) => card !== name
			);
			this.selectedCards = filteredCards;
			this.$emit("remove-card", name);
		},
		checkIfActive(name) {
			const filteredCards = this.selectedCards.filter(
				(card) => card === name
			);
			return filteredCards.length;
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
	height: 100px;
	width: 100vw;
	border: 1px solid black;
	position: fixed;
	top: 0;
	left: 0;
	display: flex;
	flex-direction: column;
}
#all-cards {
	flex: 0.3;
	width: 100%;
	display: flex;
}
#selected-cards {
	flex: 0.7;
	width: 100%;
	display: flex;
}
.card-div {
	width: 200px;
	display: flex;
	justify-content: center;
	align-items: center;
}
.unselected {
	border: 1px solid black;
}
.selected {
	border: 1px dotted black;
}
.change-cards-btn {
	align-self: flex-start;
}
.change-cards-btn:hover {
	cursor: pointer;
}
</style>
