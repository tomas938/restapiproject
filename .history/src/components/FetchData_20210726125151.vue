<template>
	<filters
		@africa="checkaf()"
		@america="checkam()"
		@asia="checkas()"
		@europe="checkeu()"
		@oceania="checkoce()"
	></filters>
	<!-- @click="$emit('getData', country)" -->

	<div v-if="mounted && !africa && !america && !asia && !europe && !oceania">
		<ul class="grid">
			<li v-for="country in countries" :key="country" @click="log">
				<country-view
					:flag="country.flag"
					:name="country.name"
					:population="country.population"
					:region="country.region"
					:capital="country.capital"
				>
				</country-view>
			</li>
		</ul>
	</div>

	<div v-if="africa">
		<ul class="grid">
			<li v-for="country in checkAfrica" :key="country.name" @click="some">
				<country-view
					:flag="country.flag"
					:name="country.name"
					:population="country.population"
					:region="country.region"
					:capital="country.capital"
				>
				</country-view>
			</li>
		</ul>
	</div>
	<div v-if="america">
		<ul class="grid">
			<li v-for="country in checkAmerica" :key="country.name">
				<country-view
					:flag="country.flag"
					:name="country.name"
					:population="country.population"
					:region="country.region"
					:capital="country.capital"
				>
				</country-view>
			</li>
		</ul>
	</div>
	<div v-if="asia">
		<ul class="grid">
			<li v-for="country in checkAsia" :key="country.name">
				<country-view
					:flag="country.flag"
					:name="country.name"
					:population="country.population"
					:region="country.region"
					:capital="country.capital"
				>
				</country-view>
			</li>
		</ul>
	</div>
	<div v-if="europe">
		<ul class="grid">
			<li v-for="country in checkEurope" :key="country.index">
				<country-view
					:flag="country.flag"
					:name="country.name"
					:population="country.population"
					:region="country.region"
					:capital="country.capital"
				>
				</country-view>
			</li>
		</ul>
	</div>
	<div v-if="oceania">
		<ul class="grid">
			<li v-for="country in checkOceania" :key="country.name">
				<country-view
					:flag="country.flag"
					:name="country.name"
					:population="country.population"
					:region="country.region"
					:capital="country.capital"
				>
				</country-view>
			</li>
		</ul>
	</div>
</template>
<script>
import filters from "../components/FilteringCoutnry.vue";
import CountryView from "../views/CountryView.vue";
export default {
	emits: ["getData"],
	components: {
		CountryView,
		filters,
	},
	data() {
		return {
			info: null,
			mounted: null,
			countries: [],
			clicked: false,
			africa: false,
			america: false,
			asia: false,
			europe: false,
			oceania: false,
			countrydata: null,
			country: [],
		};
	},
	mounted() {
		fetch("https://restcountries.eu/rest/v2/all")
			.then((res) => res.json())
			.then((data) => (this.countries = data))
			.catch((err) => console.log(err.message));
		this.mounted = true;
	},
	computed: {
		checkAfrica() {
			return this.countries.filter((country) => country.region === "Africa");
		},
		checkAmerica() {
			return this.countries.filter((country) => country.region === "Americas");
		},
		checkAsia() {
			return this.countries.filter((country) => country.region === "Asia");
		},
		checkEurope() {
			return this.countries.filter((country) => country.region === "Europe");
		},
		checkOceania() {
			return this.countries.filter((country) => country.region === "Oceania");
		},
	},
	methods: {
		log(country) {
			console.log(country);
		},
		getData(country) {
			console.log(country);
		},
		// countryData(
		// 	item,
		// 	population,
		// 	region,
		// 	subregion,
		// 	capital,
		// 	domain,
		// 	currencies,
		// 	lang,
		// 	border
		// ) {
		// 	this.country = [
		// 		item,
		// 		population,
		// 		region,
		// 		subregion,
		// 		capital,
		// 		domain,
		// 		currencies,
		// 		lang,
		// 		border,
		// 	];

		// 	this.$emit("countryData", this.country);
		// },

		changeVisibility() {
			this.clicked = !this.clicked;
		},
		checkaf() {
			this.oceania = false;
			this.europe = false;
			this.asia = false;
			this.america = false;
			this.africa = true;
		},
		checkam() {
			this.oceania = false;
			this.europe = false;
			this.asia = false;
			this.africa = false;
			this.america = true;
		},
		checkas() {
			this.oceania = false;
			this.europe = false;
			this.africa = false;
			this.america = false;
			this.asia = true;
		},
		checkeu() {
			this.oceania = false;
			this.asia = false;
			this.africa = false;
			this.america = false;
			this.europe = true;
		},
		checkoce() {
			this.asia = false;
			this.africa = false;
			this.america = false;
			this.europe = false;
			this.oceania = true;
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
	grid-template-columns: repeat(4, auto);
	padding: 0 7rem 7rem 7rem;
	grid-gap: 7rem;

	li {
		overflow: hidden;
		border-radius: 5px;
		background-color: $darkblue-el;
		box-shadow: 5px 5px 15px 5px rgba(0, 0, 0, 0.19);
		list-style: none;
		color: $white;
		display: grid;
		grid-template-rows: repeat(2, 170px);
	}
}
</style>
