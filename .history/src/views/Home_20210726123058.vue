<template>
	<navigation-bar></navigation-bar>
	<fetch-data @get-data="log()"></fetch-data>
	<card :name="this.clickedCountry.name"> </card>
</template>

<script>
// @ is an alias to /src
import NavigationBar from "../components/NavigarionBar.vue";
import FetchData from "../components/FetchData.vue";
import Card from "../views/Card.vue";
// :currencies="this.clickedCountry.currencies[0].name"
// :languages="this.clickedCountry.languages[0].name
// :name="this.clickedCountry.name"
// 	:native="this.clickedCountry.nativeName"
// 	:population="this.clickedCountry.population"
// 	:languages="this.clickedCountry.languages"
// 	:region="this.clickedCountry.region"
// 	:subregion="this.clickedCountry.subregion"
// 	:capital="this.clickedCountry.capital"
// 	:topLevelDomain="this.clickedCountry.topLevelDomain"
// 	:borders="this.clickedCountry.borders"

export default {
	components: {
		NavigationBar,
		FetchData,
		Card,
	},
	data() {
		return {
			clickedCountry: {},
		};
	},

	name: "Home",
	methods: {
		log(countryData) {
			// this.clickedCountry = countryData;
			// console.log(this.clickedCountry);
			console.log(countryData);
		},
	},
};
</script>
