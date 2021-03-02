<template>
    <div class="tarefas">
        <h1 class="titulo-campo">Criar nova tarefa</h1>
        <cria-tarefa />

        <h1 class="titulo-tarefa">Tarefas</h1>
        <div class="lista">
            <template v-if="tarefas.length">
                <tarefa v-for="tarefa in tarefas" :key="tarefa.nome" :tarefa="tarefa" />
            </template>
            <template v-else>
                <h2>Nenhuma tarefa para realizar :)</h2>
            </template>
        </div>
    </div>
</template>

<script>
import Tarefa from '@/components/tarefa'
import CriaTarefa from '@/components/criaTarefas'

export default {
    components:{Tarefa, CriaTarefa},
    props: {
        tarefas: {type: Array, required: true}
    }    
}
</script>

<style scoped>
.tarefas{
    width: 600px;
    border: 0.4px solid #FFF;
    padding: 20px;
    display: grid;
    grid-template-areas: "titulo-campo" "campo" "titulo-tarefa" "lista";
}

.tarefas h1{
    display: inline;
    margin: 0 auto;
    position: relative;
    padding-bottom: 5px;
    color: #FFF;
    text-transform: uppercase;
}

.tarefas .titulo-campo{
    grid-area: titulo-campo;
}

.tarefas .titulo-tarefa{
    grid-area: titulo-tarefa;
}

.tarefas h1::after{
    content: '';
    position: absolute;
    width: 100%;
    height: 3px;
    background: #FFF;
    left: 0;
    bottom: 0;
}

.tarefas .lista{
    grid-area: lista;
    margin-top: 20px;
}

.tarefas .lista h2{
    display: block;
    margin: 0 auto;
    text-align: center;
    color: rgba(0,0,0,0.5);
}
</style>