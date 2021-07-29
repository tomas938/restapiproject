<template>
	<router-link to="/"></router-link>
	<router-link to="/card"></router-link>
	<router-view />
</template>
<script>
export default {};
</script>
<style lang="scss">
@import "@/assets/_variables.scss";
* {
	margin: 0;
	padding: 0;
	box-sizing: border-box;
	font-family: $font-primary;
	color: $white;
}
html {
	font-size: 62.5%;
}
.container {
	max-width: 1440px;
}
body {
	height: 100vh;
	// background-color: hsl(207, 26%, 17%);
}
</style>
