<script setup>
import Header from './components/Header.vue';
import CreateTask from './components/CreateTask.vue';
import HowToUse from './components/HowToUse.vue';
import Footer from './components/Footer.vue';
</script>

<template>
	<Header />
	<CreateTask />
	<HowToUse />
	<Footer />
</template>

<style lang="scss">
@import './assets/sass/01-settings/settings';
@import './assets/sass/03-generic/reset';
</style>
