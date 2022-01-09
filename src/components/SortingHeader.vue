<template>
	<div id="outer-container">
		<div v-for="(card, index) in cards" class="card-div" :key="index">
			{{ card.name }} Sort
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
	justify-content: center;
	align-items: center;
}
.card-div {
	border: 1px solid black;
    flex: 1;
    height: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
}
</style>
