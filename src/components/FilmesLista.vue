<template>
  <div class="row">
      <!-- coluna 1 -->
      <div class="col-8">
        <h2>Filmes</h2>   
          <FilmesListaIten 
            v-for="filme in filmes"
            :key="filme.id" 
            v-bind="filme"> 
          </FilmesListaIten>
    </div>

    <!-- coluna 2 -->
    <div class="col-4">
      <FilmesListaItenInfo/>
    </div>
  </div>
</template>

<script>

import FilmesListaIten from './FilmesListaIten.vue'
import FilmesListaItenInfo from './FilmesListaItenInfo.vue'

export default {
  components: {
    FilmesListaIten,
    FilmesListaItenInfo
  },
  data(){
    return {
      filmes:[
        { id: 1, titulo:'Vinguladores: Guerra infinita', ano: 2021},
        { id: 2, titulo:'Homem formiga e a Vespa', ano: 2021},
        { id: 3, titulo:'Pantera Negra', ano: 2021 }
      ]
    }
  }
}
</script>
