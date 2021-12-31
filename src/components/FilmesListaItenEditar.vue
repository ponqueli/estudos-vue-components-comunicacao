<template>
    <div>
        <h2>Editar filme</h2>

        <div class="form-group">
            <label>Título:</label>
            <input 
                type="text" 
                class="form-control"
                placeholder="Insira o título"
                :value="filmeSelecionado.titulo"
                @input="filmeSelecionado = { propriedade:'titulo', valor: $event.target.value }">
        </div>

        <div class="form-group">
            <label>Ano:</label>
            <input 
                type="text" 
                class="form-control"
                placeholder="Insira o Ano"
                :value="filmeSelecionado.ano"
                @input="filmeSelecionado = { propriedade:'ano', valor: $event.target.value }">
        </div>

        <div class="form-group">
            <label>Diretor:</label>
            <input 
                type="text" 
                class="form-control"
                placeholder="Insira o diretor"
                :value="filmeSelecionado.diretor"
                @input="filmeSelecionado = { propriedade:'diretor', valor: $event.target.value }">
        </div>
        
        <div class="float-left">
            <button @click="salvarFilme" class='btn btn-primary' >Salvar</button>
        </div>
    </div>
</template>
<script>

import { eventBus } from './../main'

export default {
    props:{
        filme:{
            type: Object,
            required: true
        }
    },
    data(){
        return{
            filmeLocal: this.filme
        }
    },
    computed:{
        filmeSelecionado:{
            set(dados){
                this.filmeLocal = Object.assign(
                    {},
                    this.filmeLocal,
                    { [dados.propriedade]: dados.valor }
                )
            },
            get(){
                return this.filme
            }
        },

    },
    watch: {
        filme(novoFilme) { // crie o watcher na prop "filme"
            this.filmeLocal = Object.assign({}, novoFilme)
        }
    },
    methods:{
        salvarFilme(){
            eventBus.atualizarFilme(this.filmeLocal)
        }
    }
}
</script>