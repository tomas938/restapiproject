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
	a {
		color: rgb(179, 179, 179);
		text-decoration: none;
	}
}
</style>
