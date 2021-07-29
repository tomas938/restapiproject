<template>
	<img :src="`${flag}`" alt="" />
	<div class="text">
		<h3 class="country-name">{{ name }}</h3>
		<h4><span>Population:</span> {{ population }}</h4>
		<h4 class="country-region"><span>Region:</span> {{ region }}</h4>
		<h4><span>Capital:</span> {{ capital }}</h4>
	</div>
</template>

<script>
export default {
	props: ["flag", "name", "population", "region", "capital"],
};
</script>

<style lang="scss" scoped>
@import "@/assets/_variables.scss";
img {
	width: 100%;
	height: 100%;
	object-fit: cover;
}
.text {
	padding: 2rem 3rem 0rem 3rem;
	text-align: left;

	@media only screen and (max-width: 1300px) {
		padding: 2rem 3rem 5rem 3rem;
	}
	@media only screen and (max-width: 600px) {
		margin-bottom: 5rem;
	}
	color: black;
}
h3 {
	font-weight: $bold;
	padding-bottom: 1rem;
	font-size: 2rem;
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
	font-size: 1.4rem;
	@media only screen and (max-width: 600px) {
		font-size: 1.9rem;
	}

	font-weight: $light;
	line-height: 2.4rem;
	@media only screen and (max-width: 600px) {
		line-height: 3.2rem;
	}
	color: $verylight-bg;
}
span {
	font-weight: $medium;

	color: $white;
}

a {
	text-decoration: none;
	color: $white;
}
</style>
