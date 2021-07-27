<template>
	<div class="container__btn">
		<div class="container__btn__wrapper">
			<router-link to="/">Back</router-link>
			<div class="arrow"></div>
		</div>
	</div>
</template>

<script>
export default {};
</script>

<style lang="scss" scoped>
@import "@/assets/_variables.scss";
.container__btn {
	width: 12rem;
	padding: 1rem 3rem;
	margin: 8rem 0 8rem 0;
	background-color: $darkblue-el;
	box-shadow: 5px 5px 15px 5px rgba(0, 0, 0, 0.32);
	@media only screen and (max-width: 850px) {
		margin-left: 10%;
		margin-top: 4rem;
		margin-bottom: 4rem;
	}
	@media only screen and (max-width: 410px) {
		width: 7rem;
		font-size: 1.4rem;
		margin: 1rem 0 1rem 0;
		margin-left: 10%;
		padding: 0.5rem 1rem;
	}
	a {
		color: rgb(179, 179, 179);
		text-decoration: none;
	}
}
</style>
