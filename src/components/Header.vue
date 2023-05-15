<script setup></script>

<template>
	<header class="menu">
		<section class="menu__controls">
			<a class="menu__logo" href="#">To Do List</a>

			<button class="menu__btn menu__btn--open">
				<i class="menu__icon bx bx-menu-alt-right"></i>
			</button>
			<button class="menu__btn menu__btn--close menu__btn--hide">
				<i class="menu__icon bx bx-x"></i>
			</button>
		</section>
		<nav class="menu__navbar menu__navbar--hide">
			<a href="#" class="menu__link">¿Cómo usar?</a>
			<a href="#" class="menu__link">Crear tarea</a>
		</nav>
	</header>
</template>

<style lang="scss" scoped>
@use '../assets/sass/02-tools/layout';
@import '../assets/sass/01-settings/settings';
.menu {
	padding: 1em 0.5em;
	position: sticky;
	top: 0em;

	background-color: blueviolet;

	&__controls {
		display: grid;
		grid-template-columns: repeat(2, max-content);
		justify-content: space-between;
	}
	&__btn {
		@include layout.square(2em);
		grid-column: 2/3;
		grid-row: 1/2;

		transition: $transition-time transform ease-in-out;

		&--hide {
			transform: scale(0);
		}
	}
	&__icon {
		font-size: 2em;
	}
	&__logo {
		@include layout.flex-center();
		font-size: 1.3em;
	}

	&__navbar {
		background-color: green;
		padding: 1em 0em;
		@include layout.flex(column, nowrap, space-around, center, 0.5em);

		transition: $transition-time all ease-out;

		&--hide {
			max-height: 0em;
			padding: 0em 0em;
			overflow: hidden;
		}
	}
}
</style>
