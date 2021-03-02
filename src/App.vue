<template>
  <div id="app">
    <progresso :progresso="progresso"/>
    <lista-tarefas :tarefas="listaTarefas"/>
  </div>
</template>

<script>
import Progresso from '@/components/progresso'
import ListaTarefas from '@/components/listaTarefas'
import barramento from '@/barramento'

export default {
  name: 'App',
  components:{
    ListaTarefas,
    Progresso
  },
  data(){
    return {
      listaTarefas:[]
    }
  },
  watch:{
    listaTarefas: {
      deep: true,
      handler(){
        localStorage.setItem('tarefas', JSON.stringify(this.listaTarefas))
      }
    }
  },
  methods:{
    adicionarTarefa(tarefa){
      const nomeIgual = t => t.nome === tarefa.nome
      const isIgual = this.listaTarefas.filter(nomeIgual).length == 0

      if(isIgual){
        this.listaTarefas.push({
          nome: tarefa.nome,
          pendente: tarefa.pendente || true
        })
      }
    },
    removerTarefa(tarefa){
      const index = this.listaTarefas.indexOf(tarefa)
      if(index >= 0){
        this.listaTarefas.splice(index, 1)
      }
    }
  },
  computed:{
    progresso(){
      const total = this.listaTarefas.length
      const feitos = this.listaTarefas.filter(t => !t.pendente).length
      
      return Math.round(feitos / total * 100) || 0
    }
  },
  created(){
    const storage = JSON.parse(localStorage.getItem('tarefas'))
    if(Array.isArray(storage)){
      this.listaTarefas = storage
    }
    else{
      this.listaTarefas = []
    }
    
    barramento.$on('tarefaAdicionada', tarefa => this.adicionarTarefa(tarefa))
    barramento.$on('tarefaDeletada', tarefa => this.removerTarefa(tarefa))
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@300;400;700&display=swap');
*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body{
  width: 100%;
  height: 100vh;
  font-family: 'Roboto', sans-serif;
}

#app{
  width: 100%;
  height: 100%;
  background: #11998e;  /* fallback for old browsers */
  background: -webkit-linear-gradient(to right, #38ef7d, #11998e);  /* Chrome 10-25, Safari 5.1-6 */
  background: linear-gradient(to right, #38ef7d, #11998e); /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */



  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
</style>
