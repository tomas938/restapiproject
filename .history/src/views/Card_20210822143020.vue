<template>
	<div class="overlay">
		<div class="container">
			<back-button @click="$emit('close')"></back-button>
			<div class="container__content">
				<div class="container__content__img">
					<img :src="`${flag}`" alt="" />
				</div>
				<div class="container__content__description">
					<h1>{{ name }}</h1>
					<div class="container__country__information">
						<div class="left">
							<h3>
								Native Name: <span>{{ native }}</span>
							</h3>
							<h3>
								Population: <span>{{ numberWithCommas(population) }}</span>
							</h3>
							<h3>
								Region: <span>{{ region }}</span>
							</h3>
							<h3>
								Sub Region: <span>{{ subregion }}</span>
							</h3>
							<h3>
								Capital: <span>{{ capital }}</span>
							</h3>
						</div>
						<div class="right">
							<h3>
								Top Level Domain:
								<span>{{ topLevelDomain[0] }}</span>
							</h3>
							<h3>
								Currencies: <span>{{ currencies[0].name }}</span>
							</h3>
							<h3>
								Language: <span>{{ languages[0].name }}</span>
							</h3>
						</div>
					</div>
					<div class="borders">
						<span>Border Countries:</span>
						<a v-for="border in borders" :key="border">{{ border }}</a>
						<a v-if="borders.length === 0">None</a>
					</div>
				</div>
			</div>
		</div>
	</div>
</template>

<script>
import backButton from "./Backbutton.vue";
export default {
	components: {
		backButton,
	},
	props: [
		"name",
		"native",
		"population",
		"flag",
		"region",
		"subregion",
		"capital",
		"topLevelDomain",
		"currencies",
		"languages",
		"borders",
	],

	data() {
		return {
			country: null,
		};
	},
	numberWithCommas(population) {
		if (population)
			return population.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",");
	},
};
</script>

<style lang="scss" scoped>
@import "@/assets/_variables.scss";

.overlay {
	position: fixed;
	top: 0%;
	left: 50%;
	width: 100%;
	height: 100vh;
	transform: translateX(-50%);
	background: rgba(0, 0, 0, 0.904);
}
.container {
	padding: 0 10rem;
	@media only screen and (max-width: 850px) {
		padding: 0 5rem;
	}
	@media only screen and (max-width: 390px) {
		padding: 0 2rem;
	}

	margin: 0 auto;
	color: $white;
	font-size: 1.5rem;
	@media only screen and (max-width: 1100px) {
		font-size: 1.2rem;
	}
	@media only screen and (max-width: 1000px) {
		font-size: 1rem;
	}
	@media only screen and (max-width: 850px) {
		font-size: 2rem;
	}
	&__content {
		display: flex;
		justify-content: space-between;
		gap: 5rem;
		@media only screen and (max-width: 850px) {
			align-items: center;
			flex-direction: column;
			justify-items: flex-start;
		}
		@media only screen and (max-width: 1100px) {
			gap: 0rem;
		}

		&__img {
			width: 45%;
			@media only screen and (max-width: 850px) {
				width: 80%;
			}
			img {
				width: 100%;
				height: 100%;
			}
		}
	}
	&__content__description {
		width: 45%;
		@media only screen and (max-width: 850px) {
			width: 80%;
		}
		display: flex;
		flex-direction: column;
		justify-content: space-around;
	}
	&__country__information {
		display: flex;
		justify-content: space-between;
		@media only screen and (max-width: 850px) {
			flex-direction: column;
		}
	}
	.borders {
		@media only screen and (max-width: 1250px) {
			display: grid;
			grid-gap: 0.7rem;
			grid-template-rows: repeat(1, 1fr);
			grid-template-columns: repeat(3, 1fr);
		}
		@media only screen and (max-width: 410px) {
			grid-gap: 0rem;
		}

		span {
			grid-column: 1/4;
			padding: 0 1rem 0 0;
			font-weight: $medium;
			@media only screen and (max-width: 410px) {
				font-size: 1.4rem;
			}
		}
		a {
			@media only screen and (max-width: 1250px) {
				text-align: center;
			}
			background-color: $darkblue-el;
			padding: 1rem 2rem;
			margin-right: 1rem;
			color: white;
			box-shadow: 5px 5px 15px 5px rgba(0, 0, 0, 0.32);
			font-weight: $light;
			@media only screen and (max-width: 600px) {
				margin-top: 1rem;
				padding: 1rem 0.5rem;
				margin-right: 0.5rem;
			}
			@media only screen and (max-width: 850px) {
				font-size: 1.4rem;
				padding: 0.5rem 0.5rem;
			}
		}
	}
}
h3 {
	font-size: 1.6rem;
	font-weight: $medium;
	line-height: 3rem;
	@media only screen and (max-width: 1000px) {
		font-size: 1.2rem;
	}
	@media only screen and (max-width: 850px) {
		font-size: 2rem;
		line-height: 3.5rem;
	}
	@media only screen and (max-width: 650px) {
		line-height: 2.5rem;
		font-size: 1.5rem;
	}
	@media only screen and (max-width: 410px) {
		font-size: 1.2rem;
		line-height: 2rem;
	}
}
h1 {
	@media only screen and (max-width: 850px) {
		margin-top: 3rem;
	}
	@media only screen and (max-width: 410px) {
		margin-top: 0.8rem;
	}
	@media only screen and (max-width: 410px) {
		font-size: 2.7rem;
	}
}
a {
	text-decoration: none;
	color: $white;
}
span {
	font-weight: $light;
}
</style>
