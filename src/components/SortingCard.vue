<template>
	<div id="outer-container">
		<h1 id="heading">{{ activeCard }} Sort</h1>
		<ul id="description">
			<li
				v-for="bullet in bulletPoints"
				class="description-item"
				:key="bullet"
			>
				{{ bullet }}
			</li>
		</ul>
		<div id="sort-numbers">
			<transition-group :name="changeAnimationSpeed">
				<li
					v-for="number in numbers"
					:class="number.isFocused ? chosenFocus : 'number-div'"
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
				<p>Animation Speed: {{ displayCurrentSpeed }}</p>
			</div>
			<button
				type="button"
				class="btn"
				:disabled="btnPressed || isSorted"
				@click="chosenAlgorithm"
			>
				Sort
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
		<p v-show="isSorted">Sort Complete!</p>
	</div>
</template>

<script>
export default {
	name: "SortingCard",
	props: {
		startingNumbers: {
			type: Array,
			required: true,
		},
		activeCard: {
			type: String,
			required: true,
		},
		bulletPoints: {
			type: Array,
			required: true,
		},
		isShown: {
			type: Boolean,
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
		changeAnimationSpeed() {
			return this.speed === 1
				? "number-list-medium"
				: this.speed === 4
				? "number-list-fast"
				: "number-list-slow";
		},
		displayCurrentSpeed() {
			return this.speed === 1
				? "Medium"
				: this.speed === 4
				? "Fast"
				: "Slow";
		},
		chosenAlgorithm() {
			return this.activeCard === "Bubble"
				? this.startBubbleSort
				: this.activeCard === "Insertion"
				? this.startInsertionSort
				: this.activeCard === "Selection"
				? this.startSelectionSort
				: this.startShellSort;
		},
		chosenFocus() {
			return this.activeCard === "Insertion"
				? "number-div-focused-green"
				: "number-div-focused-grey";
		},
	},
	methods: {
		async startBubbleSort() {
			let madeSwap;
			this.btnPressed = true;
			do {
				madeSwap = false;
				for (let i = 0; i < this.numbers.length; i++) {
					// sets focused to show where program is looking for search
					this.numbers[i].isFocused = true;
					if (this.numbers[i + 1]?.isFocused === false) {
						this.numbers[i + 1].isFocused = true;
					}
					await new Promise((r) => setTimeout(r, 300 / this.speed));

					// perform swap of adjacent numbers
					if (this.numbers[i + 1]?.value < this.numbers[i].value) {
						const holdingValue = this.numbers[i + 1];
						this.numbers[i + 1] = this.numbers[i];
						this.numbers[i] = holdingValue;
						madeSwap = true;
						this.numberOfSwaps++;
						// from top answer https://stackoverflow.com/questions/951021/what-is-the-javascript-version-of-sleep
						await new Promise((r) =>
							setTimeout(r, 1100 / this.speed)
						);
					}
					this.numbers[i].isFocused = false;
				}
				if (madeSwap) {
					this.iterations++;
				}
			} while (madeSwap);
			this.btnPressed = false;
			this.isSorted = true;
		},
		async startInsertionSort() {
			this.btnPressed = true;
			// first element is always already sorted
			this.numbers[0].isFocused = true;
			for (let i = 1; i < this.numbers.length; i++) {
				this.numbers[i].isFocused = true;
				let madeSwap = false;
				let currentValue = this.numbers[i].value;
				let j = i - 1;
				while (j >= 0 && this.numbers[j].value > currentValue) {
					const holdingValue = this.numbers[j + 1];
					this.numbers[j + 1] = this.numbers[j];
					this.numbers[j] = holdingValue;
					madeSwap = true;
					this.numberOfSwaps++;
					j--;
					await new Promise((r) => setTimeout(r, 1100 / this.speed));
				}
				this.numbers[j + 1].value = currentValue;
				if (madeSwap) {
					this.iterations++;
				}
			}
			// remove green focus
			for (let i = 0; i < this.numbers.length; i++) {
				this.numbers[i].isFocused = false;
			}
			this.btnPressed = false;
			this.isSorted = true;
		},
		async resetNumbers() {
			this.numbers = JSON.parse(JSON.stringify(this.startingNumbers));
			// so buttons aren't pressed until reset complete
			await new Promise((r) => setTimeout(r, 1100 / this.speed));
			this.isSorted = false;
			this.iterations = 0;
			this.numberOfSwaps = 0;
		},
		async startSelectionSort() {
			// based off https://stackabuse.com/selection-sort-in-javascript/
			this.btnPressed = true;
			for (let i = 0; i < this.numbers.length; i++) {
				let lowest = i;

				for (let j = i + 1; j < this.numbers.length; j++) {
					this.numbers[i].isFocused = true;
					this.numbers[j].isFocused = true;

					if (this.numbers[j].value < this.numbers[lowest].value) {
						lowest = j;
					}
					await new Promise((r) => setTimeout(r, 1100 / this.speed));
				}

				// remove focus after each iteration
				for (let k = 0; k < this.numbers.length; k++) {
					this.numbers[k].isFocused = false;
				}

				if (lowest != i) {
					this.numberOfSwaps++;
					const holdingValue = this.numbers[i];
					this.numbers[i] = this.numbers[lowest];
					this.numbers[lowest] = holdingValue;
				}
				this.iterations++;
			}
			this.btnPressed = false;
			this.isSorted = true;
		},
		async startShellSort() {
			// based off https://learnersbucket.com/tutorials/algorithms/shell-sort-algorithm-in-javascript/
			this.btnPressed = true;
			for (
				let interval = this.numbers.length / 2;
				interval >= 1;
				interval /= 2
			) {
				for (let i = interval; i < this.numbers.length; i += 1) {
					let holdingValue = this.numbers[i];
					let j;
					this.numbers[i].isFocused = true;

					for (
						j = i;
						j >= interval &&
						this.numbers[j - interval].value > holdingValue.value;
						j -= interval
					) {
						this.numbers[j - interval].isFocused = true;
						await new Promise((r) =>
							setTimeout(r, 1100 / this.speed)
						);

						this.numbers[j] = this.numbers[j - interval];
						this.numberOfSwaps++;
					}
					this.numbers[i].isFocused = false;
					this.numbers[j] = holdingValue;
				}
				this.iterations++;
				// remove focus after each iteration
				for (let k = 0; k < this.numbers.length; k++) {
					this.numbers[k].isFocused = false;
				}
			}
			this.btnPressed = false;
			this.isSorted = true;
		},
		changeSpeed() {
			if (this.speed === 0.5) {
				return (this.speed = 1);
			} else if (this.speed === 1) {
				return (this.speed = 4);
			} else {
				return (this.speed = 0.5);
			}
		},
	},
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
@import "../assets/styles/variables.css";

#outer-container {
	height: 375px;
	width: 575px;
	box-shadow: 2px 3px 10px var(--light-black);
	padding: 10px;
	border-radius: 15px;
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
#sort-numbers {
	display: flex;
	height: 50px;
	width: 90%;
	border: 3px solid black;
	margin: auto;
}
.number-div,
.number-div-focused-grey,
.number-div-focused-green {
	list-style: none;
	display: flex;
	flex: 1;
	justify-content: center;
	align-items: center;
	border: 1px dotted var(--light-black);
}
.number-div-focused-grey {
	font-size: 1.3rem;
	background-color: var(--light-grey);
}
.number-div-focused-green {
	background-color: var(--light-green);
}
.number-list-medium-move {
	transition: all 1s ease-in-out;
	background-color: var(--light-red);
}
.number-list-slow-move {
	transition: all 2s ease-in-out;
	background-color: var(--light-red);
}
.number-list-fast-move {
	transition: all 0.25s ease-in-out;
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
	transform: scale(1);
}
</style>
