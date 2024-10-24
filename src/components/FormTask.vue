<script setup>
const props = defineProps(["handleAddTask", "tempTask", "handleChangingFilter", "handleTaskTitle"])
</script>

<template>
	<form @submit.prevent="props.handleAddTask">
		<div class="row">
			<div class="col">
				<input
					@change="props.handleTaskTitle"
					required
					class="form-control"
					type="text"
					placeholder="Digite aqui sua tarefa"
					:value="props.tempTask" />
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
					@change="handleChangingFilter"
					class="form-control">
					<option value="todas">Todas as tarefas</option>
					<option value="pendentes">Pendentes</option>
					<option value="finalizadas">Finalizadas</option>
				</select>
			</div>
		</div>
	</form>
</template>
