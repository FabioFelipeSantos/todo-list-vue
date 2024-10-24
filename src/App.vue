<script setup>
import { reactive } from "vue"
import HeaderTask from "./components/HeaderTask.vue"
import FormTask from "./components/FormTask.vue"
import TaskList from "./components/TaskList.vue"

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

function handleFilter(event) {
	state.filter = event.target.value
}

function handleTaskTitle(event) {
	state.tempTask = event.target.value
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
		<HeaderTask
			:pendingTasks="getIncompleteTask().length"
			:allTasks="state.tasks.length" />
		<FormTask
			:handleAddTask="handleAddTask"
			:tempTask="state.tempTask"
			:handleChangingFilter="handleFilter"
			:handleTaskTitle="handleTaskTitle" />
		<TaskList :filteredTasks="getFilteredTask()" />
	</div>
</template>
