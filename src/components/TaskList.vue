<script setup>
const props = defineProps(["filteredTasks"])
</script>

<template>
	<ul class="list-group mt-4">
		<h3 v-if="props.filteredTasks.length === 0">Não há tarefas pendentes!</h3>
		<li
			v-else
			class="list-group-item"
			v-for="task in props.filteredTasks"
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
</template>

<style scoped>
.done {
	text-decoration: line-through;
}
</style>
