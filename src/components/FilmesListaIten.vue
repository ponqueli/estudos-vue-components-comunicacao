<template>
    <li class="list-group-item d-flex flex-row align-items-center">
        <span class='me-auto'>{{ filme.titulo }} - {{ filme.ano }}</span>
        <button @click="selecionar" type="button" class="text-white btn btn-secondary">Selecionar</button>
    </li>
</template>
<script>

import { eventBus } from './../main'

export default {
    props: {
        filme:{
            type: Object,
            required: true
        }  
    },
    methods: {
        selecionar(){
            //this.$emit('selecionarFilme', this.filme)
            eventBus.selecionarFilme(this.filme)
        }
    }
}
</script>