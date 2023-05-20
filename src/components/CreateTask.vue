<script setup>
import { ref, onMounted, watch } from 'vue';

const tasks = ref([]);
const newTask = ref('');

const saveTasks = () => {
	localStorage.setItem('tasks', JSON.stringify(tasks.value));
};
const loadTasks = () => {
	const savedTasks = localStorage.getItem('tasks');
	if (savedTasks) {
		tasks.value = JSON.parse(savedTasks);
	}
};

const addTask = () => {
	if (newTask.value) {
		const task = {
			id: tasks.value.length + 1,
			title: newTask.value,
			state: false,
		};
		tasks.value.push(task);
		saveTasks(), (newTask.value = '');
	}
};
const removeTask = (taskId) => {
	const index = tasks.value.findIndex((task) => task.id === taskId);
	if (index !== -1) {
		tasks.value.splice(index, 1);
	}
};

onMounted(loadTasks);

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
@use '../assets/sass/02-tools/layout';
@use '../assets/sass/02-tools/effect';
@import '../assets/sass/01-settings/settings';
.tasks {
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
		@include layout.flex(row, nowrap, space-between, center);
	}
	&__input {
		width: 85%;
		padding: 0.3em 1em;
		border-bottom: 2px solid black;
		outline: none;
	}
	&__btn {
		@include layout.square(1.3em);
	}
	&__icon {
		font-size: 1.3em;
	}
}
.task {
	padding: 1em 0.5em;
	border-top: $box-border;
	@include layout.flex(row, nowrap, space-between, center);

	&--completed {
		background-color: rgba(172, 255, 47, 0.1);
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
