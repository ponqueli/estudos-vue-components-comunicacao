<template>
  <div class="row">
      <!-- coluna 1 -->
      <div class="col-8">
        <h2>Filmes</h2>   
          <ul class="list-group list-group-flush">
            <FilmesListaIten 
              v-for="filme in filmes"
              :key="filme.id" 
              :filme="filme"
              :class="aplicarClasseAtiva(filme)"
              @selecionarFilme="filmeSelecionado = $event"> 
            </FilmesListaIten>
          </ul>
          <div class="alert alert-success" v-show="mostrarAlerta">
            O Filme foi salvo com sucesso!
          </div>
    </div>

    <!-- coluna 2 -->
    <div class="col-4">
      <FilmesListaItenInfo 
        v-if="!editar"
        :filme="filmeSelecionado"
        @editarFilme="editarFilme"
      />

      <FilmesListaItenEditar
        v-else
        :filme="filmeSelecionado"/>
    </div>
  </div>
</template>

<script>
import { eventBus } from './../main'

import FilmesListaIten from './FilmesListaIten.vue'
import FilmesListaItenInfo from './FilmesListaItenInfo.vue'
import FilmesListaItenEditar from './FilmesListaItenEditar.vue'

export default {
  components: {
    FilmesListaIten,
    FilmesListaItenEditar,
    FilmesListaItenInfo
  },
  data(){
    return {
      filmes:[
        { id: 1, titulo:'Vinguladores: Guerra infinita', ano: 2021, diretor: 'Stan Lee'},
        { id: 2, titulo:'Homem formiga e a Vespa', ano: 2021, diretor: 'Stan Lee'},
        { id: 3, titulo:'Pantera Negra', ano: 2021, diretor: 'Stan Lee' }
      ],
      filmeSelecionado: undefined,
      editar: false,
      mostrarAlerta: false
    }
  },
  methods: {
    aplicarClasseAtiva(filmeIterado){
      return {
        active: this.filmeSelecionado && this.filmeSelecionado.id === filmeIterado.id
      }
    },
    editarFilme(filme){
      this.editar = true
      this.filmeSelecionado = filme
    },
    atualizarFilme(filmeAtualizado){
      const indice = this.filmes.findIndex(filme => filme.id === filmeAtualizado.id )
      this.filmes.splice(indice, 1, filmeAtualizado);
      this.mostrarAlerta = true;
      this.filmeSelecionado = undefined;
      this.editar = false;
      setTimeout(() => this.mostrarAlerta = false, 2000);
    }
  },
  created(){
    eventBus.$on('selecionarFilme', (filmeSelecionado)=>{
        this.filmeSelecionado = filmeSelecionado
    })
    eventBus.$on('atualizarFilme',this.atualizarFilme)
  }
}
</script>
