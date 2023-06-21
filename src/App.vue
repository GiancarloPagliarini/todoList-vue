<script setup>
import { reactive } from 'vue';
import Cabecalho from './components/Cabecalho.vue';
import Formulario from './components/Formulario.vue';
import TaskList from './components/TaskList.vue';

const estado = reactive({
  tarefaTemp: '',
  filtro: 'todas',
  tarefas: [
    {
      titulo: "Estudar VueJS",
      finalizada: false,
    },
  ]
})

const getTarefasPendentes = () => {
  return estado.tarefas.filter(tarefa => !tarefa.finalizada)
}

const getTarefasFinalizadas = () => {
  return estado.tarefas.filter(tarefa => tarefa.finalizada)
}

const getTarefasFiltradas = () => {
  const { filtro } = estado

  switch (filtro) {

    case "pendentes":
      return getTarefasPendentes()

    case "finalizadas":
      return getTarefasFinalizadas()

    default:
      return estado.tarefas
  }
}

const cadastraTarefa = () => {
  const novaTarefa = {
    titulo: estado.tarefaTemp,
    finalizada: false,
  }

  estado.tarefas.push(novaTarefa)
  estado.tarefaTemp = '';
}

</script>

<template>
  <div class="container">
    <Cabecalho :tarefas-pendentes="getTarefasPendentes().length"/>
    <Formulario :trocar-filtro="event => estado.filtro = event.target.value" :tarefa-temp="estado.tarefaTemp" :edita-tarefa-temp="event => estado.tarefaTemp = event.target.value" :cadastra-tarefa="cadastraTarefa"/>
    <TaskList :tarefas="getTarefasFiltradas()"/>
  </div>
</template>