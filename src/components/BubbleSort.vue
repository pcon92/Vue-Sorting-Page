<template>
	<div id="outer-container">
		<h1 id="heading">Bubble Sort</h1>
		<ul id="description">
			<li class="description-item">Steps through list</li>
			<li class="description-item">Compares adjacent elements</li>
			<li class="description-item">
				Swaps them if they are in wrong order
			</li>
		</ul>
		<div id="bubble-sort-numbers">
			<transition-group :name="speedChanged">
				<li
					v-for="number in numbers"
					class="number-div"
					:key="number.id"
				>
					{{ number.value }}
				</li>
			</transition-group>
		</div>
		<div>
			<div id="stats">
				<p>Iterations: {{ iterations }}</p>
				<p>Number of Swaps: {{ numberOfSwaps }}</p>
				<p>Speed: {{ speed === 1 ? 'Medium' : speed === 1.5 ? 'Fast' : 'Slow' }}</p>
			</div>
			<button
				type="button"
				class="btn"
				:disabled="btnPressed || isSorted"
				@click="startBubbleSort"
			>
				Bubble Sort
			</button>
			<button
				type="button"
				class="btn"
				:disabled="btnPressed || !isSorted"
				@click="resetNumbers"
			>
				Reset
			</button>
			<button
				type="button"
				class="btn"
				:disabled="btnPressed || isSorted"
				@click="changeSpeed"
			>
				Change Speed
			</button>
		</div>
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
			iterations: 0,
			numberOfSwaps: 0,
			btnPressed: false,
			isSorted: false,
			speed: 1,
		};
	},
	computed: {
		speedChanged() {
			return this.speed === 1 ? 'number-list-medium' : this.speed === 1.5 ? 'number-list-fast' : 'number-list-slow';
		}
	},
	methods: {
		async startBubbleSort() {
			let madeSwap;
			this.btnPressed = true;
			this.iterations = 0;
			do {
				madeSwap = false;
				for (let i = 0; i < this.numbers.length; i++) {
					if (this.numbers[i + 1]?.value < this.numbers[i].value) {
						const holdingValue = this.numbers[i + 1];
						this.numbers[i + 1] = this.numbers[i];
						this.numbers[i] = holdingValue;
						madeSwap = true;
						this.numberOfSwaps++;
						// from top answer https://stackoverflow.com/questions/951021/what-is-the-javascript-version-of-sleep
						await new Promise((r) => setTimeout(r, 1100/this.speed));
					}
				}
				if (madeSwap) {
					this.iterations++;
				}
			} while (madeSwap);
			this.btnPressed = false;
			this.isSorted = true;
		},
		resetNumbers() {
			this.numbers = JSON.parse(JSON.stringify(this.startingNumbers));
			this.isSorted = false;
			this.iterations = 0;
			this.numberOfSwaps = 0;
		},
		changeSpeed() {
			if (this.speed === 0.5) {
				return this.speed = 1;
			} else if (this.speed === 1) {
				return this.speed = 1.5;
			} else {
				return this.speed = 0.5;
			}
		},
	},
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
@import "../assets/styles/variables.css";

#outer-container {
	height: 350px;
	width: 500px;
	border: 1px solid black;
	box-shadow: 3px 3px 10px var(--light-black);
	padding: 10px;
	border-radius: 5px;
	text-align: center;
}
#heading {
	text-decoration: underline;
}
#description {
	text-align: left;
}
.description-item {
	font-family: var(--font-family);
}
#bubble-sort-numbers {
	display: flex;
	height: 50px;
	width: 90%;
	border: 3px solid black;
	margin: auto;
}
.number-div {
	list-style: none;
	display: flex;
	flex: 1;
	justify-content: center;
	align-items: center;
	border: 1px dotted var(--light-black);
	background-color: white;
	transition-property: background-color;
}
.number-list-medium-move {
	transition: all 1s ease-in-out;
	background-color: var(--light-red);
}
.number-list-slow-move {
	transition: all 1.5s ease-in-out;
	background-color: var(--light-red);
}
.number-list-fast-move {
	transition: all 0.5s ease-in-out;
	background-color: var(--light-red);
}
#stats {
	display: flex;
	justify-content: space-evenly;
}
.btn {
	height: 30px;
	width: 120px;
	margin: 10px;
	border-radius: 5px;
}
.btn:hover {
	cursor: pointer;
	transform: scale(1.05);
}
.btn:disabled {
	cursor: not-allowed;
}
</style>
