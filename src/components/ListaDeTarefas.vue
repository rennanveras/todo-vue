<script setup>
    const props = defineProps(['tarefasFiltradas', 'titulo']);
</script>

<template>
    <ul class="list-group mt-4">
        <li class="list-group-item" v-for="tarefa in props.tarefasFiltradas" v-if="props.tarefasFiltradas.length > 0">
            <input @change="evento => tarefa.finalizada = evento.target.checked" :checked="tarefa.finalizada === true" :id="tarefa.titulo" type="checkbox">
            <label :class="{ done: tarefa.finalizada }" class="ms-3" :for="tarefa.titulo">
                {{ tarefa.titulo }}
            </label>
        </li>
        <h5 v-else>Não tem terefas {{ titulo }}</h5>
    </ul>
</template>

<style scoped>
    .done{
        text-decoration: line-through;
    }
</style>