<template>
	<filters
		@search-icon-clicked="checkCountry"
		@enter-pressed="checkCountry"
		@africa="checkaf"
		@america="checkam"
		@asia="checkas"
		@europe="checkeu"
		@oceania="checkoce"
	>
	</filters>
	<div>
		<ul class="grid ">
			<li
				v-for="country in searchedCountry"
				:key="country.name"
				@click="itemClicked(country), $emit('clicked')"
			>
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
	<div v-if="mounted && !africa && !america && !asia && !europe && !oceania">
		<ul class="grid">
			<li
				v-for="country in countries"
				:key="country.name"
				@click="itemClicked(country), $emit('clicked')"
			>
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
			<li
				v-for="country in checkAfrica"
				:key="country.name"
				@click="itemClicked(country)"
			>
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
			<li
				v-for="country in checkAmerica"
				:key="country.name"
				@click="itemClicked(country)"
			>
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
			<li
				v-for="country in checkAsia"
				:key="country.name"
				@click="itemClicked(country)"
			>
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
		<ul class="grid ">
			<li
				v-for="country in checkEurope"
				:key="country.index"
				@click="itemClicked(country)"
			>
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
			<li
				v-for="country in checkOceania"
				:key="country.name"
				@click="itemClicked(country)"
			>
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
	emits: ["getData", "clicked"],
	components: {
		CountryView,
		filters,
	},
	data() {
		return {
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
			searchedCountry: "",
			addCoutnry: false,
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
		checking() {
			return (
				this.countries.filter(
					(country) => country.name === this.searchedCountry
				),
				console.log(this.searchedCountry)
			);
		},
	},
	methods: {
		checkCountry(inputedcountry) {
			this.searchedCountry = inputedcountry;
			this.searchedCountry = this.countries.filter(
				(country) => country.name === this.searchedCountry
			);
			console.log(this.searchedCountry);
		},

		itemClicked(country) {
			this.$emit("getData", country);
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
	grid-template-columns: repeat(4, 1fr);
	@media only screen and (max-width: 1300px) {
		grid-gap: 3rem;
	}
	@media only screen and (max-width: 1100px) {
		padding: 0 2rem 2rem 2rem;
	}
	@media only screen and (max-width: 1000px) {
		grid-template-columns: repeat(2, auto);
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
		color: $white;
		display: grid;
		grid-template-rows: repeat(2, 170px);
		cursor: pointer;
		@media only screen and (max-width: 600px) {
			padding-bottom: 5rem;
		}
	}
}
</style>
