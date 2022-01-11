<template>
	<div id="outer-container">
		<div id="all-cards">
			<li v-for="(card, index) in cards" class="card-div unselected" :key="index">
				{{ card.name }} Sort
			</li>
		</div>
		<div id="selected-cards">
			<li v-for="(card, index) in cards" class="card-div selected" :key="index">
				{{ card.name }} Sort
			</li>
		</div>
	</div>
</template>

<script>
export default {
	props: ["cards"],
	data() {
		return {
			sortingWidgets: ["bubbleSort", "insertionSort"],
		};
	},
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#outer-container {
	height: 100px;
	width: 100vw;
	border: 1px solid black;
	position: absolute;
	top: 0;
	left: 0;
	display: flex;
	flex: 1;
	flex-direction: column;
	justify-content: center;
	align-items: center;
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
	border: 1px solid black;
	width: 100px;
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
</style>
