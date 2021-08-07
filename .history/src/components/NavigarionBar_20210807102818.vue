<template>
	<header :class="{ white: toggleTheme }">
		<nav class="navigation">
			<div class="navigation__logo">
				<h1>Where in the world?</h1>
			</div>
			<div class="navigation__mode" @click="toggle">
				<svg
					xmlns="http://www.w3.org/2000/svg"
					enable-background="new 0 0 24 24"
					height="24px"
					viewBox="0 0 24 24"
					width="24px"
					fill="#000000"
				>
					<g><rect fill="none" height="24" width="24" /></g>
					<g>
						<g>
							<path
								d="M15.5,22c1.05,0,2.05-0.16,3-0.46c-4.06-1.27-7-5.06-7-9.54s2.94-8.27,7-9.54C17.55,2.16,16.55,2,15.5,2 c-5.52,0-10,4.48-10,10S9.98,22,15.5,22L15.5,22z"
							/>
						</g>
					</g>
				</svg>
				<h2>{{ toggleTheme ? "Light Mode" : "Dark mode" }}</h2>
			</div>
		</nav>
	</header>
</template>

<script>
export default {
	emits: ["toggleColor"],
	data() {
		return {
			toggleTheme: false,
		};
	},
	methods: {
		toggle() {
			this.toggleTheme = !this.toggleTheme;
			this.$emit("toggleColor");
		},
	},
};
</script>

<style lang="scss" scoped>
@import "@/assets/_variables.scss";

header {
	width: 100%;
	color: $white;
	background-color: $darkblue-el;
	text-shadow: 4px -1px 5px rgba(0, 0, 0, 0.48);
	box-shadow: -5px -2px 12px 5px #000000;
	.navigation {
		height: 10rem;
		width: 90%;
		margin: auto;
		display: flex;
		justify-content: space-between;
		align-items: center;
	}
	.navigation__mode {
		cursor: pointer;
		display: flex;
		justify-content: space-around;
		align-items: center;
	}
	svg {
		margin-right: 1rem;
		transform: rotate(320deg);
		fill: $white;
	}
	h1 {
		font-size: 3rem;
		font-weight: $bold;
		@media only screen and (max-width: 700px) {
			font-size: 2rem;
		}
		@media only screen and (max-width: 500px) {
			font-size: 1.7rem;
		}
		@media only screen and (max-width: 320px) {
			font-size: 1.5rem;
		}
	}
	h2 {
		font-weight: $medium;
		@media only screen and (max-width: 500px) {
			font-size: 1.5rem;
		}
		@media only screen and (max-width: 320px) {
			font-size: 1.3rem;
		}
	}
}
.white {
	text-shadow: 0px 0px 0px rgba(0, 0, 0, 0.48);
	border-bottom: 3px solid #f5f1f1;

	svg {
		fill: $darkblue-text;
	}
	h1 {
		color: $darkblue-text;
	}
	h2 {
		color: $darkblue-text;
	}
}
</style>
