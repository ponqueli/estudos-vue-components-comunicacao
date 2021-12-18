<template>
    <ul class='list-group'>
        <li class="list-group-item d-flex flex-row align-items-center">
            <span class='me-auto'>{{ filmeTituloConcatenado }} - {{ ano }}</span>
            <button type="button" class="btn btn-secondary float-right disabled ">Selecionar</button>
        </li>
    </ul>
</template>
<script>
export default {
    props: {
        titulo: {
            type: String,
            required: true
            
        },
        ano:{
            type: Number,
            required: true
        }
       
    },
    computed:{
        filmeTituloConcatenado(){
            return `Título: ${this.titulo}` 
        }
    }
}
</script>