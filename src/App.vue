<script setup>
	import { ref, computed, nextTick } from "vue";

	const isDarkTheme = ref();

	// Checks what theme if by default set by user

	const darkTheme = ref(
		window
			.matchMedia("(prefers-color-scheme: dark)")
			.addEventListener("change", (e) => {
				const colorScheme = e.matches ? "dark" : "light";
				isDarkTheme.value = colorScheme === "dark" ? true : false;
				console.log(
					colorScheme,
					window.matchMedia("(prefers-color-scheme)")
				);
			})
	);

	// Changing color scheme on click

	const themes = {
		dark: {
			"--color-bg": "#212626",
			"--color-font": "#cddede",
		},
		light: {
			"--color-bg": "#fff",
			"--color-font": "#3c3a3d",
		},
	};

	const changeTheme = () => {
		if (isDarkTheme.value === true) {
			isDarkTheme.value = false;
		} else {
			isDarkTheme.value = true;
		}

		const theme = ref(
			themes[isDarkTheme.value === true ? "dark" : "light"]
		);

		for (let i in theme.value) {
			document.documentElement.style.setProperty(i, theme.value[i]);
		}
	};
</script>

<template>
	<div class="container" :class="isDarkTheme ? 'dark' : 'light'">
		<h1>Current theme is: {{ isDarkTheme ? "dark" : "light" }} theme</h1>
	</div>
	<button @click="changeTheme">Change theme</button>
</template>

<style lang="scss" scoped>
	.container {
		width: 500px;
		height: 300px;
		display: flex;
		justify-content: center;
		align-items: center;
		color: var(--color-font);
		background-color: var(--color-bg);
	}
</style>
