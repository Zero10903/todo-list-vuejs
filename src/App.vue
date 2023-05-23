<script setup>
// Importación de componentes
import Header from './components/Header.vue';
import CreateTask from './components/CreateTask.vue';
import HowToUse from './components/HowToUse.vue';
import Footer from './components/Footer.vue';
</script>

<template>
	<div class="main">
		<Header />
		<CreateTask />
		<aside class="aside">
			<HowToUse />
			<Footer />
		</aside>
	</div>
</template>

<style lang="scss" scoped>
@import './assets/sass/01-settings/settings';
@import './assets/sass/03-generic/reset';

@media (min-width: 1024px) {
	// Layout Grid para Desktop version
	.main {
		margin-inline: 2em;
		display: grid;
		grid-template-columns: repeat(3, 1fr);
		grid-template-areas:
			'header header header'
			'aside create-task create-task'
			'aside create-task create-task'
			'aside create-task create-task';
		gap: 20px;
	}
	.menu {
		grid-area: header;
	}
	.aside {
		grid-area: aside;
	}
	.tasks {
		height: 100%;
		margin: 0;
		grid-area: create-task;
	}
}
</style>
