<script setup>
const props = defineProps(['tarefas'])
</script>

<template>
    <ul class="list-group mt-4">
        <li class="list-group-item" v-for="tarefa in props.tarefas">
            <input @change="event => tarefa.finalizada = event.target.checked" :checked="tarefa.finalizada" type="checkbox"
                :id="tarefa.titulo">
            <label class="ms-3" :class="{ done: tarefa.finalizada }" :for="tarefa.titulo">
                {{ tarefa.titulo }}
            </label>
        </li>
    </ul>
</template>

<style scoped>
.done {
    text-decoration: line-through;
}
</style>
