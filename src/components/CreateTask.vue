<script setup>
import { ref, onMounted, watch } from 'vue';

// Variable que almacena la lista de tareas
const tasks = ref([]);
// Variable que almacena una nueva tarea
const newTask = ref('');

// Función que guarda la lista en el localStorage
const saveTasks = () => {
	localStorage.setItem('tasks', JSON.stringify(tasks.value));
};
// Función que carga en la web la lista de tareas, obteniendola del localStorage
const loadTasks = () => {
	const savedTasks = localStorage.getItem('tasks');
	if (savedTasks) {
		tasks.value = JSON.parse(savedTasks);
	}
};

// Función que añade una nueva tarea a la lista
const addTask = () => {
	if (newTask.value) {
		const task = {
			id: tasks.value.length + 1,
			title: newTask.value,
			state: false, // Define si la tarea fue completada o no (estña enlazada con el checkbox con un v-model)
		};
		tasks.value.push(task); //Actualizamos la lista de tareas
		saveTasks(); //Subimos la lista al localStorage
		newTask.value = ''; //Vaciamos la variable que contenia la nueva tarea para poder reusarla
	}
};
// Función que remueve una tarea de la lista
const removeTask = (taskId) => {
	const index = tasks.value.findIndex((task) => task.id === taskId);
	if (index !== -1) {
		tasks.value.splice(index, 1);
	}
};
// Carga la lista obtenida del localStorage en la web al montarla
onMounted(loadTasks);

// Función que vigila los cambios en la lista de tareas y la sube automaticamente al localStorage
watch(
	tasks,
	() => {
		saveTasks();
	},
	{ deep: true }
);
</script>
<template>
	<section class="tasks">
		<h2 class="tasks__title">Tareas</h2>
		<!-- Sección para crear nuevas tareas -->
		<form class="tasks__create" @submit.prevent="addTask">
			<input
				class="tasks__input"
				v-model="newTask"
				type="text"
				placeholder="Titulo de la tarea..."
			/>
			<button class="tasks__btn" type="submit">
				<i class="tasks__icon bx bx-plus"></i>
			</button>
		</form>
		<!-- Sección para mostrar las tareas existentes -->
		<ul class="tasks__list">
			<li
				class="task"
				:class="{ 'task--completed': task.state }"
				v-for="task in tasks"
				:key="task.id"
			>
				<h3 :class="{ 'task__title--completed': task.state }">
					{{ task.title }}
				</h3>
				<div class="task__controls">
					<input class="task__btn" type="checkbox" v-model="task.state" />
					<button class="task__btn" @click="removeTask(task.id)">
						<i class="task__icon bx bx-x"></i>
					</button>
				</div>
			</li>
		</ul>
	</section>
</template>

<style lang="scss" scoped>
// Mixins que aceleran el proceso de estilizado
@use '../assets/sass/02-tools/layout';
// Mixins que crean efectos rapidamente
@use '../assets/sass/02-tools/effect';
// Variables de sass
@import '../assets/sass/01-settings/settings';
.tasks {
	height: 65vh;
	margin: 1em 0.5em;
	border: $box-border;
	border-radius: $box-radius;
	@include effect.glass($box-blur);

	&__title {
		padding: 1em 0em;
		font-size: 1.5em;
		text-align: center;
	}
	&__create {
		padding: 1em;
		border-top: $box-border;
		border-bottom: $box-border;
		@include layout.flex(row, nowrap, space-between, center);
	}
	&__input {
		width: 85%;
		padding: 0.3em 1em;
		border-bottom: 2px solid black;
		outline: none;

		&::placeholder {
			color: black;
		}
	}
	&__btn {
		@include layout.square(1.3em);
	}
	&__icon {
		font-size: 1.3em;
	}
	&__list {
		max-height: 44vh;

		overflow-y: auto;
		&::-webkit-scrollbar {
			width: 5px;
		}
		&::-webkit-scrollbar-thumb {
			background-color: $color-principal;
		}
		&::-moz-scrollbar {
			width: thin;
		}
		&::-moz-scrollbar-thumb {
			scrollbar-color: $color-principal;
		}
	}
}
.task {
	padding: 1em 0.5em;
	accent-color: $color-secundario;
	&:not(:first-child) {
		border-top: $box-border;
	}
	@include layout.flex(row, nowrap, space-between, center);

	&--completed {
		background-color: $color-principal-transparente;
	}

	&__title--completed {
		text-decoration: line-through;
	}
	&__controls {
		@include layout.flex-center(1em);
	}
	&__btn {
		@include layout.square(1.3em);
	}
	&__icon {
		font-size: 1.3em;
	}
}
</style>
