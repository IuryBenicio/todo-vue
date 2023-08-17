<template>
    <ul class="list-group mt-4">
        <li class="list-group-item" v-for="tarefa in getTarefasFiltradas()">
            <input @change="evento => tarefa.finalizadas = evento.target.checked" :checked="tarefa.finalizadas"
                :id="tarefa.titulo" type="checkbox">
            <label :class="{ done: tarefa.finalizadas }" class="ms-3" :for="tarefa.titulo">
                {{ tarefa.titulo }}
            </label>
        </li>
    </ul>
</template>