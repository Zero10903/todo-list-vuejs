<script setup></script>
<template>
	<section class="how">
		<h2>Cómo usar:</h2>
		<ul class="how__list">
			<li class="how__item">Escriba su tarea en el input.</li>
			<li class="how__item">
				Presione el botón de + a la derecha del input o la tecla Enter para
				agregar la tarea a la lista.
			</li>
			<li class="how__item">
				Marque la tarea como completada cuando la misma sea realizada.
			</li>
			<li class="how__item">
				Elimine una tarea usando la X cuando desee quitarla de la lista.
			</li>
		</ul>
	</section>
</template>
<style lang="scss" scoped>
@use '../assets/sass/02-tools/effect';
@import '../assets/sass/01-settings/settings';
.how {
	margin: 0em 0.5em;
	padding: 1em 0.5em;
	border: $box-border;
	border-radius: $box-radius;
	@include effect.glass($box-blur);

	&__item {
		padding: 0.5em;
		border-top: $box-border;
		list-style-type: disc;
		list-style-position: inside;
	}
}
</style>
