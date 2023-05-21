<script setup></script>
<template>
	<footer class="footer">
		<article class="footer__contact">
			<h2 class="footer__title">Contáctanos</h2>
			<a href="http://instagram.com/wickedness__delirium" target="_blank"
				>Instagram</a
			>
			<a href="mailto:sam.alejandro.bustos@gmail.com" target="_blank">Gmail</a>
			<a href="http://github.com/Zero10903" target="_blank">Github</a>
		</article>
	</footer>
</template>

<style lang="scss" scoped>
// Mixins que aceleran el proceso de estilizado
@use '../assets/sass/02-tools/layout';
// Mixins que crean efectos rapidamente
@use '../assets/sass/02-tools/effect';
// Variables de sass
@import '../assets/sass/01-settings/settings';
.footer {
	margin: 0.5em;
	border: $box-border;
	border-radius: $box-radius;
	@include effect.glass($box-blur);

	&__contact {
		padding: 1em;
		@include layout.flex(column, wrap, center, center, 0.5em);
	}
	&__title {
		padding-bottom: 0.5em;
		font-size: 1.5em;
		text-align: center;
	}
}
@media (min-width: 1024px) {
	.footer {
		height: fit-content;
	}
}
</style>
