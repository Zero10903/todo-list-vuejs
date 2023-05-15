<script setup></script>

<template>
	<header class="menu">
		<p class="menu__logo">To Do List</p>
		<nav class="menu__navbar">
			<a href="#" class="menu__link">¿Cómo usar?</a>
			<a href="#" class="menu__link">Crear tarea</a>
		</nav>
	</header>
</template>

<style lang="scss" scoped>
.menu {
	padding: 1em 0.5em;
	position: sticky;
	top: 0em;

	display: grid;
	grid-template-columns: repeat(2, max-content);
	justify-content: space-between;

	background-color: blueviolet;

	&__logo {
		font-size: 1.3em;
	}

	&__navbar {
		display: flex;
		flex-flow: row nowrap;
		justify-content: space-around;
		align-items: center;
		gap: 0.5em;
	}
}
</style>
