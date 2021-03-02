<template>
    <div :class="['item-lista', estadoTarefa]" @click="tarefa.pendente = !tarefa.pendente">
        <h3>{{ tarefa.nome }}</h3>
        <span @click.stop="retirarItem()">X</span>
    </div>
</template>

<script>
import barramento from '@/barramento'

export default {
    props:{
        tarefa: {type: Object, required: true}
    },
    data(){
        return{}
    },
    methods:{
        retirarItem(){
            barramento.$emit('tarefaDeletada', this.tarefa)
        }
    },
    computed: {
        estadoTarefa(){
            return {
                fazer: this.tarefa.pendente,
                feito: !this.tarefa.pendente
            }
        }
    }
}
</script>

<style scoped>
.item-lista{
    width: 100%;
    padding: 15px;
    position: relative;
    border-bottom: 2px solid #000;
    margin-bottom: 10px;
    cursor: pointer;
    transition: transform 0.3s ease;
}

.item-lista:hover{
    transform: scale(1.01);
    transition: transform 0.3s ease;
}

.item-lista.feito{
    background: #11998e
}
.item-lista.feito h3{
    text-decoration: line-through;
}

.item-lista.fazer {
    background: crimson;
}

.item-lista h3{
    color: #FFF;
    text-transform: uppercase;
}

.item-lista span{
    position: absolute;
    right: 5px;
    top: 50%;
    cursor: pointer;
    color: #FFF;
    padding: 5px;
    font-weight: 700;
    transform: translateY(-50%);
}
</style>