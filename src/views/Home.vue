<template>
	<navigation-bar></navigation-bar>

	<fetch-data @get-data="log"></fetch-data>
	<card
		v-if="clicked"
		@close="showCard"
		:flag="this.clickedCountry.flag"
		:name="this.clickedCountry.name"
		:native="this.clickedCountry.nativeName"
		:population="this.clickedCountry.population"
		:region="this.clickedCountry.region"
		:subregion="this.clickedCountry.subregion"
		:capital="this.clickedCountry.capital"
		:currencies="this.clickedCountry.currencies"
		:languages="this.clickedCountry.languages"
		:topLevelDomain="this.clickedCountry.topLevelDomain"
		:borders="this.clickedCountry.borders"
	>
	</card>
</template>

<script>
import NavigationBar from "../components/NavigarionBar.vue";
import FetchData from "../components/FetchData.vue";
import Card from "../views/Card.vue";
export default {
	components: {
		NavigationBar,
		FetchData,
		Card,
	},
	data() {
		return {
			clickedCountry: {},
			clicked: null,
		};
	},

	name: "Home",
	methods: {
		log(country) {
			this.clickedCountry = country;
			this.clicked = !this.clicked;
		},
		showCard() {
			this.clicked = !this.clicked;
		},
	},
};
</script>
