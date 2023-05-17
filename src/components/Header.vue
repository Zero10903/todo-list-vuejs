<script setup>
import { ref, computed } from 'vue';
const countMenu = ref(false);

const toggleMenu = () => {
	countMenu.value = !countMenu.value;
};

const openBtnClass = computed(() => ({
	'': countMenu.value == false,
	'menu__btn--hide': countMenu.value == true,
}));
const closeBtnClass = computed(() => ({
	'menu__btn--hide': countMenu.value == false,
	'': countMenu.value == true,
}));
const menuClass = computed(() => ({
	'menu__navbar--hide': countMenu.value == false,
	'': countMenu.value == true,
}));
</script>

<template>
	<header class="menu">
		<section class="menu__controls">
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
			<a href="#" class="menu__link">¿Cómo usar?</a>
			<a href="#" class="menu__link">Crear tarea</a>
		</nav>
	</header>
</template>

<style lang="scss" scoped>
@use '../assets/sass/02-tools/layout';
@use '../assets/sass/02-tools/effect';
@import '../assets/sass/01-settings/settings';
.menu {
	margin: 0.5em 0.5em auto 0.5em;
	padding: 1em 0.5em;
	position: sticky;
	top: 0.5em;
	z-index: 999;

	border: $box-border;
	border-radius: $box-radius;

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
</style>
