<script setup>
  import { reactive } from 'vue';
  import Cabecalho from './components/Cabecalho.vue';
  import Formulario from './components/Formulario.vue';
  import ListaDeTarefas from './components/ListaDeTarefas.vue';

  const estado = reactive({
    filtro: 'todas',
    tarefaTemp: '',
    tarefas: [
      {
        titulo: "Estudar ES6",
        finalizada: false,
      },
      {
        titulo: "Ler livros de programação",
        finalizada: false,
      },
      {
        titulo: "Fazer exercícios do curso",
        finalizada: false,
      }
    ]
  })

  const getTarefasPendentes = () => {
    return estado.tarefas.filter(tarefa => !tarefa.finalizada)
  }

  const getTarefasFinalizadas = () => {
    return estado.tarefas.filter(tarefa => tarefa.finalizada)
  }

  const getTarefasFiltadras = () => {
    const { filtro } = estado;

    switch(filtro){
      case 'pendentes':
        return getTarefasPendentes();
      case 'finalizadas': 
        return getTarefasFinalizadas();
      default:
        return estado.tarefas;
    }
  }

  const cadastraTarefa = () => {
    const tarefaNova = {
      titulo: estado.tarefaTemp,
      finalizada: false,
    }
    estado.tarefas.push(tarefaNova)
    estado.tarefaTemp = '';
  }
</script>

<template>
  <div class="container">
    <Cabecalho :tarefas-pendentes="getTarefasPendentes().length"/>
    <Formulario :trocar-filtro="e => estado.filtro = e.target.value" :tarefa-temp="estado.tarefaTemp" :edita-tarefa-temp="e => estado.tarefaTemp = e.target.value" :cadastra-tarefa="cadastraTarefa" />
    <ListaDeTarefas :tarefas-filtradas="getTarefasFiltadras()" :titulo="estado.filtro" />
    
  </div>
</template>


