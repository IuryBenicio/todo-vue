<script setup>
import { reactive } from 'vue';


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
    <header class="p-5 mb-4 mt-4 bg-light rounded-3">
      <h1>olá</h1>
      <p>
        vocÊ possui {{ getTarefasPendentes.length }} tarefas pendentes
      </p>        
    </header>
    <form @submit.prevent="cadastraTarefa">
      <div class="row">
        <div class="col">
          <input :value="estado.tarefaTemporaria" @change="evento => estado.tarefaTemporaria = evento.target.value" required type="text" placeholder="Digite aqui a descrição da tarefa" class="form-control">
        </div>
        <div class="col-md-2">
          <button type="submit" class="btn btn-primary">cadastrar</button>
        </div>
        <div class="col-md-2">
          <select @change="evento => estado.filtro = evento.target.value" class="form-control">
            <option value="todas">todas as tarefas</option>
            <option value="pendentes">pendentes</option>
            <option value="finalizadas">finalizadas</option>
          </select>
        </div>
      </div>
    </form>
    {{ estado.filtro }}
    <ul class="list-group mt-4">
      <li class="list-group-item" v-for="tarefa in getTarefasFiltradas()">
        <input @change="evento => tarefa.finalizadas = evento.target.checked" :checked="tarefa.finalizadas" :id="tarefa.titulo" type="checkbox">
        <label :class="{ done: tarefa.finalizadas }" class="ms-3" :for="tarefa.titulo">
          {{ tarefa.titulo }}
        </label>
      </li>
    </ul>
  </div>

</template>

<style scoped>
.done{
  text-decoration: line-through;
}
</style>
