<template>
	<h2>Bubble Sort</h2>
	<ul>
		<li>Steps through list</li>
		<li>Compares adjacent elements</li>
		<li>Swaps them if they are in wrong order</li>
	</ul>
	<div id="bubble-sort-numbers">
		<li v-for="(number, index) in numbers" class="number-div" :key="index">
			{{ number }}
		</li>
	</div>
	<div>
		<button @click="startBubbleSort">Bubble Sort</button>
		<button @click="resetNumbers">Reset</button>
	</div>
</template>

<script>
export default {
	name: "BubbleSort",
	props: {
		startingNumbers: {
			type: Array,
			required: true,
		},
	},
	data() {
		return {
			// JSON methods used to 'deep copy' array allowing reset to prop values
			numbers: JSON.parse(JSON.stringify(this.startingNumbers)),
		};
	},
	methods: {
		async startBubbleSort() {
			let madeSwap;
			do {
				madeSwap = false;
				for (let i = 0; i < this.numbers.length; i++) {
					if (this.numbers[i + 1] < this.numbers[i]) {
						const holdingValue = this.numbers[i + 1];
						this.numbers[i + 1] = this.numbers[i];
						this.numbers[i] = holdingValue;
						madeSwap = true;
						// from top answer https://stackoverflow.com/questions/951021/what-is-the-javascript-version-of-sleep
						await new Promise((r) => setTimeout(r, 250));
					}
				}
			} while (madeSwap);
		},
		resetNumbers() {
			this.numbers = JSON.parse(JSON.stringify(this.startingNumbers));
		}
	},
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#bubble-sort-numbers {
	display: flex;
	height: 50px;
	border: 3px solid black;
}
.number-div {
	height: 50px;
	width: 50px;
	list-style: none;
	display: flex;
	justify-content: center;
	align-items: center;
	border: 1px dotted rgba(0, 0, 0, 0.3);
}
</style>
