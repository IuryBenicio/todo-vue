<script>

</script>

<template>
    <form @submit.prevent="cadastraTarefa">
        <div class="row">
            <div class="col">
                <input :value="estado.tarefaTemporaria" @change="evento => estado.tarefaTemporaria = evento.target.value"
                    required type="text" placeholder="Digite aqui a descrição da tarefa" class="form-control">
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
</template>