<template>
	<div class="root">
		<navigation-bar @toggle-color="changeTheme"></navigation-bar>
		<div class="wrapper" :class="{ filterchange: theme }">
			<div class="search">
				<div class="search__input">
					<svg
						:class="{ svgchange: theme }"
						@click="getCoutryName"
						xmlns="http://www.w3.org/2000/svg"
						height="24px"
						viewBox="0 0 24 24"
						width="24px"
						fill="#FFFFFF"
					>
						<path d="M0 0h24v24H0V0z" fill="none" />
						<path
							d="M15.5 14h-.79l-.28-.27C15.41 12.59 16 11.11 16 9.5 16 5.91 13.09 3 9.5 3S3 5.91 3 9.5 5.91 16 9.5 16c1.61 0 3.09-.59 4.23-1.57l.27.28v.79l5 4.99L20.49 19l-4.99-5zm-6 0C7.01 14 5 11.99 5 9.5S7.01 5 9.5 5 14 7.01 14 9.5 11.99 14 9.5 14z"
						/>
					</svg>
					<input
						:class="{ inputchange: theme }"
						v-model.trim="inputedcountry"
						@keyup="getCoutryName"
						type="text"
						placeholder="Search for a country..."
					/>
				</div>
				<div class="search__filter" :class="{ filterlinks: theme }">
					<p :class="{ parachange: theme }">Filter by Region</p>
					<svg
						:class="{ svgchange: theme }"
						@click="ggg"
						xmlns="http://www.w3.org/2000/svg"
						height="24px"
						viewBox="0 0 24 24"
						width="24px"
						fill="#FFFFFF"
					>
						<path d="M24 24H0V0h24v24z" fill="none" opacity=".87" />
						<path d="M16.59 8.59L12 13.17 7.41 8.59 6 10l6 6 6-6-1.41-1.41z" />
					</svg>
					<div class="filter__links" :class="{ active: clicked, light: theme }">
						<ul>
							<li @click="checkaf" :class="{ lighttext: theme }">Africa</li>
							<li @click="checkam" :class="{ lighttext: theme }">America</li>
							<li @click="checkas" :class="{ lighttext: theme }">Asia</li>
							<li @click="checkeu" :class="{ lighttext: theme }">Europe</li>
							<li @click="checkoce" :class="{ lighttext: theme }">Oceania</li>
						</ul>
					</div>
				</div>
			</div>
		</div>

		<div :class="{ white: theme }">
			<ul class="grid">
				<li
					:class="{ white: theme }"
					v-for="country in countries"
					:key="country.name"
					@click="itemClicked(country), $emit('clicked')"
				>
					<img :src="country.flag" alt="" />
					<div class="text" :class="{ white: theme }">
						<h3 class="country-name" :class="{ white: theme }">
							{{ country.name }}
						</h3>
						<h4 :class="{ white: theme }">
							<span :class="{ white: theme }"> Population:</span
							>{{ country.population }}
						</h4>
						<h4 :class="{ white: theme }">
							<span :class="{ white: theme }">Region:</span>
							{{ country.region }}
						</h4>
						<h4 :class="{ white: theme }">
							<span :class="{ white: theme }">Capital:</span>
							{{ country.capital }}
						</h4>
					</div>
				</li>
			</ul>
		</div>
	</div>
</template>
<script>
// import filters from "../components/FilteringCoutnry.vue";
import NavigationBar from "../components/NavigarionBar.vue";

export default {
	emits: ["getData", "clicked"],
	components: {
		NavigationBar,
	},
	data() {
		return {
			mounted: null,
			countries: [],
			clicked: false,

			countrydata: null,
			country: [],
			inputedcountry: "",
			searchedCountry: "",
			addCoutnry: false,
			theme: false,
			res: null,
			coutnryName: "",
		};
	},
	async mounted() {
		this.res = await fetch("https://restcountries.eu/rest/v2/all");
		this.countries = await this.res.json();

		// console.log(this.countries);
		this.mounted = true;
	},

	methods: {
		changeVisibility() {
			this.clicked = !this.clicked;
		},
		changeTheme() {
			this.theme = !this.theme;
		},

		itemClicked(country) {
			this.$emit("getData", country);
		},
		getCoutryName() {
			this.coutnryName = document.querySelectorAll(".country-name");
			this.coutnryName.forEach((name) => {
				console.log(name.innerText);
			});
		},
	},
};
</script>

<style lang="scss" scoped>
@import "@/assets/_variables.scss";

.grid {
	max-width: 1440px;
	margin: auto;
	display: grid;
	grid-template-columns: repeat(4, 1fr);
	@media only screen and (max-width: 1300px) {
		grid-gap: 3rem;
		color: $white;
	}
	@media only screen and (max-width: 1100px) {
		padding: 0 2rem 2rem 2rem;
	}
	@media only screen and (max-width: 1000px) {
		grid-template-columns: repeat(2, 1fr);
	}
	@media only screen and (max-width: 600px) {
		grid-template-columns: repeat(1, auto);
		padding: 0 7rem 7rem 7rem;
		grid-gap: 7rem;
	}
	@media only screen and (max-width: 400px) {
		padding: 0 3rem 3rem 3rem;
	}
	@media only screen and (max-width: 320px) {
		padding: 0 1rem 1rem 1rem;
	}
	padding: 0 7rem 2.5rem 7rem;
	grid-gap: 7rem;

	li {
		overflow: hidden;
		border-radius: 5px;
		background-color: $darkblue-el;
		box-shadow: 5px 5px 15px 5px rgba(0, 0, 0, 0.19);
		list-style: none;
		display: grid;
		grid-template-rows: repeat(2, 170px);
		cursor: pointer;
		@media only screen and (max-width: 600px) {
			padding-bottom: 5rem;
		}
	}
}
.text {
	padding: 2rem 3rem 0rem 3rem;
	text-align: left;
	color: red !important;
	@media only screen and (max-width: 1300px) {
		padding: 2rem 3rem 5rem 3rem;
	}
	@media only screen and (max-width: 600px) {
		margin-bottom: -5rem;
	}
	h3 {
		font-weight: $bold;
		padding-bottom: 1rem;
		font-size: 2rem;

		.white {
			color: $darkblue-text;
		}
		@media only screen and (max-width: 1300px) {
			font-size: 1.8rem;
		}
		@media only screen and (max-width: 600px) {
			font-size: 2.4rem;
		}
		@media only screen and (max-width: 600px) {
			margin: 1rem 0 1rem 0;
		}
	}
	h4 {
		color: $white;
		font-size: 1.4rem;
		@media only screen and (max-width: 600px) {
			font-size: 1.9rem;
		}

		font-weight: $light;
		line-height: 2.4rem;
		@media only screen and (max-width: 600px) {
			line-height: 3.2rem;
		}
	}
	span {
		font-weight: $medium;
	}

	a {
		text-decoration: none;
	}
}
.white {
	background-color: white;
}
img {
	width: 100%;
	height: 100%;
	object-fit: cover;
}
.white {
	background-color: white;
	color: $darkblue-text !important;
}
.wrapper {
	width: 100%;
}
.search {
	font-size: 1.6rem;
	padding: 5rem 7rem;
	max-width: 1440px;
	margin: auto;
	display: flex;
	justify-content: space-between;
	align-items: center;
	@media only screen and (max-width: 1100px) {
		padding: 5rem 2rem;
	}
	@media only screen and (max-width: 750px) {
		flex-direction: column;
		align-items: flex-start;
	}
	&__input {
		position: relative;
		svg {
			position: absolute;
			top: 50%;
			transform: translateY(-50%);
			left: 0;
			margin: 0 2rem;
		}
	}
	input {
		border-radius: 5px;
		width: 50rem;
		@media only screen and (max-width: 550px) {
			width: 30rem;
		}
		@media only screen and (max-width: 350px) {
			width: 25rem;
			font-size: 1.2rem;
		}
		font-size: 1.6rem;
		border: none;
		outline: none;
		padding: 2rem 7rem;
		@media only screen and (max-width: 350px) {
			padding: 2rem 6rem;
		}
		background-color: $darkblue-el;
		color: $white;
		text-align: left;
		box-shadow: 5px 5px 15px 5px rgba(0, 0, 0, 0.19);
		&::placeholder {
			color: $white;
			font-weight: $light;
		}
	}
	&__filter {
		display: flex;
		justify-content: space-between;
		position: relative;
		color: $white;
		font-weight: $light;
		font-size: 1.6rem;
		border-radius: 5px;
		width: 20rem;
		padding: 1.7rem;
		box-shadow: 5px 5px 15px 5px rgba(0, 0, 0, 0.19);
		background-color: $darkblue-el;
		@media only screen and (max-width: 750px) {
			margin-top: 5rem;
		}
		@media only screen and (max-width: 350px) {
			font-size: 1.2rem;
		}
	}
	svg {
		cursor: pointer;
	}
}
.filter__links {
	padding: 2rem;
	top: 0%;
	left: 0;
	opacity: 0;
	display: block !important;
	visibility: hidden;
	width: 20rem;
	position: absolute;
	background-color: $darkblue-el;
	box-shadow: 5px 5px 15px 5px rgba(0, 0, 0, 0.19);
	border-radius: 5px;
	transition: all 0.5s ease;

	li {
		padding: 0.5rem 0;
		list-style: none;
		text-align: left;
		cursor: pointer;
	}
}
.active {
	padding: 2rem;
	top: 110%;
	opacity: 1;
	visibility: visible;
	left: 0;
	width: 20rem;
	position: absolute;
	background-color: $darkblue-el;
	box-shadow: 5px 5px 15px 5px rgba(0, 0, 0, 0.19);
	border-radius: 5px;

	li {
		padding: 0.5rem 0;
		list-style: none;
		text-align: left;
	}
}
.filterchange {
	background-color: $white;
}
.filterlinks {
	background-color: $white;
}
.search input.inputchange {
	// background-color: $input-color;
	background-color: $verylight-bg;
	color: $darkblue-text;

	&::placeholder {
		color: $darkblue-text;
	}
}
.svgchange {
	fill: $darkblue-text;
}
.parachange {
	color: $darkblue-text;
}
.light {
	background-color: $verylight-bg;
}
.lighttext {
	color: $darkblue-text;
}
.fade-enter-active,
.fade-leave-active {
	transition: opacity 0.5s ease-in-out;
}
.fade-enter-from,
.fade-leave-to {
	opacity: 0;
}
.fade-enter-to,
.fade-leave-from {
	opacity: 1;
}
</style>
