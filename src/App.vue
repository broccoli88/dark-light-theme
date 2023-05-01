<script setup>
	import { ref, computed, nextTick } from "vue";

	const isDarkTheme = ref();
	const darkTheme = ref(
		window
			.matchMedia("(prefers-color-scheme: dark)")
			.addEventListener("change", (e) => {
				const colorScheme = e.matches ? "dark" : "light";
				isDarkTheme.value = colorScheme === "dark" ? true : false;
			})
	);
</script>

<template>
	<div class="container" :class="isDarkTheme ? 'dark' : 'light'">
		<h1>Current theme is: {{ isDarkTheme ? "dark" : "light" }} theme</h1>
	</div>
</template>

<style lang="scss" scoped>
	.container {
		width: 500px;
		height: 300px;
		display: flex;
		justify-content: center;
		align-items: center;
	}
	.dark {
		color: black;
		background-color: white;
	}

	.light {
		color: white;
		background-color: black;
	}
</style>
