<script setup>
import { reactive } from "vue"

const state = reactive({
	filter: "todas",
	tempTask: "",
	tasks: [
		{
			id: 1,
			title: "Estudar ES6",
			completed: false,
		},
		{
			id: 2,
			title: "Estudar SASS",
			completed: false,
		},
		{
			id: 3,
			title: "Ir para academia",
			completed: true,
		},
	],
})

const getIncompleteTask = () => {
	return state.tasks.filter(task => !task.completed)
}

const getCompleteTask = () => {
	return state.tasks.filter(task => task.completed)
}

const getFilteredTask = () => {
	const { filter, tasks } = state

	switch (filter) {
		case "pendentes": {
			return getIncompleteTask()
		}
		case "finalizadas": {
			return getCompleteTask()
		}
		default: {
			return tasks
		}
	}
}

const handleAddTask = () => {
	const newTask = {
		id: state.tasks.length + 1,
		title: state.tempTask,
		completed: false,
	}
	state.tasks.push(newTask)
	state.tempTask = ""
}
</script>

<template>
	<div class="container">
		<header class="p-5 mb-4 mt-4 bg-light rounded-3">
			<h1>Minhas Tarefas</h1>
			<p>Você possui {{ getIncompleteTask().length }} tarefas pendentes</p>
		</header>

		<form @submit.prevent="handleAddTask">
			<div class="row">
				<div class="col">
					<input
						@change="event => (state.tempTask = event.target.value)"
						required
						class="form-control"
						type="text"
						placeholder="Digite aqui sua tarefa"
						:value="state.tempTask" />
				</div>
				<div class="col-md-2">
					<button
						type="submit"
						class="btn btn-primary w-100">
						Cadastrar
					</button>
				</div>
				<div class="col-md-2">
					<select
						@change="event => (state.filter = event.target.value)"
						name=""
						id=""
						class="form-control">
						<option value="todas">Todas as tarefas</option>
						<option value="pendentes">Pendentes</option>
						<option value="finalizadas">Finalizadas</option>
					</select>
				</div>
			</div>
		</form>
		<ul class="list-group mt-4">
			<li
				class="list-group-item"
				v-for="task in getFilteredTask()"
				:key="task.id">
				<input
					@change="event => (task.completed = event.target.checked)"
					:checked="task.completed"
					:id="`task-${task.id}`"
					type="checkbox"
					name="" />
				<label
					:class="{ done: task.completed }"
					class="ms-3"
					:for="`task-${task.id}`"
					>{{ task.title }}</label
				>
			</li>
		</ul>
	</div>
</template>

<style scoped>
.done {
	text-decoration: line-through;
}
</style>
