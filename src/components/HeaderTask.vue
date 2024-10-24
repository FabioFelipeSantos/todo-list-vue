<script setup>
const props = defineProps(["pendingTasks", "allTasks"])
</script>

<template>
	<header class="p-5 mb-4 mt-4 bg-light rounded-3">
		<h1>Minhas Tarefas</h1>
		<p>
			Você possui {{ props.pendingTasks }} tarefas pendentes de {{ props.allTasks }}. ({{
				Math.round(((props.allTasks - props.pendingTasks) * 100) / props.allTasks)
			}}% completadas)
		</p>
	</header>
</template>
