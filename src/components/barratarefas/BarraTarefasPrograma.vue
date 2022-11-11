<template>
    <div class="barratarefas-programa">
        <span 
            class="icone"
            :style="{
                backgroundImage: 'url(' + require('@/assets/icon/' + arquivoIcone + '.png') + ')'
            }"></span>
        <span class="titulo"></span>
    </div>
</template>
<script>
export default {
    name: 'paginaBarraTarefasPrograma',
    props: {
        arquivoNome: String,
        arquivoIcone: String
    },
    methods: {
        minimizarJanela() {
            this.$emit("minimizarJanela", this.arquivoNome)
        }
    }
}
</script>