<template>
	<div id="outer-container">
		<div id="links-div">
			<li v-for="link in links" class="links" :key="link.id">
				<a :href="link.url" class="icon-url-link" target="__blank"
					><i :class="link.icon"></i
				></a>
			</li>
		</div>
		<p id="footer-text">{{ name }}&nbsp; - &nbsp;{{ year }}</p>
	</div>
</template>

<script>
export default {
	props: {
		name: {
			type: String,
			required: false,
		},
		year: {
			type: String,
			required: false,
		},
		links: {
			type: Array,
			required: false,
		},
	},
	data() {
		return {};
	},
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#outer-container {
	width: 100%;
	height: 100%;
	display: flex;
	justify-content: space-around;
	align-items: center;
	box-shadow: 0px -1px 5px var(--light-black);
	z-index: 10;
	background-color: var(--background-for-footer-area);
	color: var(--white);
}
#links-div {
	display: flex;
}
.links {
	list-style: none;
	margin-right: 50px;
}
.icon-url-link {
	color: var(--white);
}
#footer-text {
	font-size: 0.8rem;
}

/* Media queries */

@media (max-width: 20rem) {
	/* 320 pixels */
	#links-div {
		transform: scale(0.8);
	}
	#footer-text {
		font-size: 0.6rem;
		min-width: 80px;
	}
}

@media (min-width: 20rem) {
	/* 320 pixels */
	#links-div {
		transform: scale(0.8);
	}
	#footer-text {
		font-size: 0.6rem;
		min-width: 80px;
	}
}

@media (min-width: 40rem) {
	/* 640 pixels */
	#links-div {
		transform: scale(0.9);
	}
	#footer-text {
		font-size: 1rem;
		min-width: 80px;
	}
}

@media (min-width: 60rem) {
	/* 960 pixels */
	#links-div {
		transform: scale(1);
	}
}
</style>
