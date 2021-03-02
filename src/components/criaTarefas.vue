<template>
    <div class="cria-tarefas">
        <input type="text" v-model="nome" @keydown.enter="adicionar()">
        <button @click="adicionar()">+</button>
    </div>
</template>

<script>
import barramento from '@/barramento'

export default {
    data(){
        return {
            nome: ''
        }
    },
    methods:{
        adicionar(){
            barramento.$emit('tarefaAdicionada', {nome: this.nome})
            this.nome = ''
        }
    }
}
</script>

<style scoped>
.cria-tarefas{
    width: 100%;
    margin: 20px 0;
    display: flex;
    align-items: center;
}

.cria-tarefas input{
    height: 35px;
    border: none;
    width: 90%;
    outline: none;
    padding-left: 10px;
    font-size: 16px;
    font-family: 'Roboto';
}

.cria-tarefas button{
    height: 35px;
    font-size: 20px;
    border: none;
    padding: 0 20px;
    width: 10%;
    font-weight: 700;
    background: #0b6945;
    color: #FFF;
    transition: background 0.3s ease-out;
    cursor: pointer;
    user-select: none;
    outline: none;
}

.cria-tarefas button:hover{
    background: rgba(0, 0, 0, 0.6);
    transition: background 0.3s ease-in;
}
</style>