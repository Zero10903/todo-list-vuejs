<script setup>
import { ref, computed } from 'vue';

// Variable booleana - Define si el menu esta abierto o no
const isMenuOpen = ref(false);

// Funcion para actualizar la variable anterior
const toggleMenu = () => {
	isMenuOpen.value = !isMenuOpen.value;
};

// Propiedad computada que define si el boton Burguer del menu se muestra o no
const openBtnClass = computed(() => ({
	'': isMenuOpen.value == false,
	'menu__btn--hide': isMenuOpen.value == true,
}));
// Propiedad computada que define si el boton X del menu se muestra o no
const closeBtnClass = computed(() => ({
	'menu__btn--hide': isMenuOpen.value == false,
	'': isMenuOpen.value == true,
}));
// Propiedad computada que define si el menu se muestra o no
const menuClass = computed(() => ({
	'menu__navbar--hide': isMenuOpen.value == false,
	'': isMenuOpen.value == true,
}));
</script>

<template>
	<header class="menu">
		<section class="menu__controls menu__controls--wide">
			<a class="menu__logo" href="#">To Do List</a>

			<button
				class="menu__btn menu__btn--open"
				:class="openBtnClass"
				@click="toggleMenu()"
			>
				<i class="menu__icon bx bx-menu-alt-right"></i>
			</button>
			<button
				class="menu__btn menu__btn--close"
				:class="closeBtnClass"
				@click="toggleMenu()"
			>
				<i class="menu__icon bx bx-x"></i>
			</button>
		</section>
		<nav class="menu__navbar" :class="menuClass">
			<a href="#" class="menu__link">Crear tarea</a>
			<a href="#" class="menu__link">¿Cómo usar?</a>
		</nav>
	</header>
</template>

<style lang="scss" scoped>
// Mixins que aceleran el proceso de estilizado
@use '../assets/sass/02-tools/layout';
// Mixins que crean efectos rapidamente
@use '../assets/sass/02-tools/effect';
// Variables de sass
@import '../assets/sass/01-settings/settings';
.menu {
	margin: 0.5em 0.5em auto 0.5em;
	padding: 1em 0.5em;
	position: sticky;
	top: 0.5em;
	z-index: 999;

	border-radius: $box-radius;

	box-shadow: $box-shadow;

	@include effect.glass($box-blur);

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
		max-height: 10em;
		padding: 2em 0em 1em;
		overflow: hidden;
		@include layout.flex(column, nowrap, space-around, center, 0.5em);

		transition: $transition-time all ease-out;

		&--hide {
			max-height: 0em;
			padding: 0em 0em;
		}
	}
}
@media (min-width: 1024px) {
	.menu {
		padding-inline: 2em;
		@include layout.flex(row, nowrap, space-between, center);
		&__btn {
			display: none;
		}
		&__navbar {
			max-height: fit-content;
			@include layout.flex(row, nowrap, space-around, center, 1em);
		}
	}
}
</style>
