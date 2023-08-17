<script setup>
  import { reactive } from 'vue';
  import Cabecalho from './components/cabecalho.vue';
  import Formulario from './components/formulario.vue';
  import Lista from './components/lista.vue';


  const estado = reactive({
    filtro:  'todas',
    tarefaTemporaria: '',
    tarefas:[
      {
        titulo: 'Estudar ES6',
        finalizadas: false
      },
      {
        titulo:  'Estudar SASS',
        finalizadas: false
      },
      {
        titulo:  'Ir para a academia',
        finalizadas: true
      },
    ]
  })

  const getTarefasPendentes = () => {
    return estado.tarefas.filter(tarefa => !tarefa.finalizadas)
  }

  const getTarefasfinalizadas = () => {
    return estado.tarefas.filter(tarefa => tarefa.finalizadas)
  }

  const getTarefasFiltradas = () => {
    const {filtro} = estado
    switch (filtro){
      case 'pendentes':
        return getTarefasPendentes();
      case 'finalizadas':
        return getTarefasfinalizadas();
      default:
        return estado.tarefas;
    }
  }

  const cadastraTarefa = ()=>{
    const tarefaNova = {
      titulo: estado.tarefaTemporaria,
      finalizadas: false,
    }
    estado.tarefas.push(tarefaNova);
    estado.tarefaTemporaria = '';
  }

</script>

<template>
  <div class="container">
    <Cabecalho :tarefas-pendentes="getTarefasPendentes().length"/>
    <Formulario :trocar-filtro="evento=>estado.filtro = evento.target.value" :tarefa-temporaria="estado.tarefaTemporaria" :editaTarefaTemporaria="evento => estado.tarefaTemporaria = evento.target.value" :cadastra-tarefas="cadastraTarefa"/>
    <lista :tarefas="getTarefasFiltradas()"/>
  </div>
</template>

