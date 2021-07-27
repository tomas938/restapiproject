<template>
	<div class="search">
		<div class="search__input">
			<svg
				@click="$emit('searchIconClicked', inputedcountry)"
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
				v-model.trim="inputedcountry"
				@keyup.enter="$emit('enterPressed', inputedcountry)"
				type="text"
				placeholder="Search for a country..."
			/>
		</div>
		<div class="search__filter">
			<p>Filter by Region</p>
			<svg
				@click="changeVisibility"
				xmlns="http://www.w3.org/2000/svg"
				height="24px"
				viewBox="0 0 24 24"
				width="24px"
				fill="#FFFFFF"
			>
				<path d="M24 24H0V0h24v24z" fill="none" opacity=".87" />
				<path d="M16.59 8.59L12 13.17 7.41 8.59 6 10l6 6 6-6-1.41-1.41z" />
			</svg>
			<div class="filter__links" :class="{ active: clicked }">
				<ul>
					<li @click="$emit('africa')">Africa</li>
					<li @click="$emit('america')">America</li>
					<li @click="$emit('asia')">Asia</li>
					<li @click="$emit('europe')">Europe</li>
					<li @click="$emit('oceania')">Oceania</li>
				</ul>
			</div>
		</div>
	</div>
</template>

<script>
export default {
	emits: [
		"africa",
		"america",
		"asia",
		"europe",
		"oceania",
		"enterPressed",
		"searchIconClicked",
	],
	data() {
		return {
			clicked: false,
			inputedcountry: "",
		};
	},
	methods: {
		changeVisibility() {
			this.clicked = !this.clicked;
		},
	},
};
</script>

<style lang="scss" scoped>
@import "@/assets/_variables.scss";

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
</style>
