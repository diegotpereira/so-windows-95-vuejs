<template>
    <div class="iniciar-menu-programa">
        <span 
            class="icone"
            :style="{
                backgroundImage: 
                'url(' + require('@/assets/icon/' + arquivoIcone + '.png') + ')'
            }">

        </span>
        <span>{{ arquivoNome }}</span>
    </div>
</template>
<script>
export default {
    name: 'paginaIniciarMenuPrograma',
    props: {
        arquivoNome: String,
        arquivoIcone: String,
        arquivoTipo: String,
        arquivos: Array
    },
    methods: {
        abrirPrograma() {
            this.$emit("abrirPrograma", this.arquivoNome, this.arquivoIcone, this.arquivoTipo, this.arquivos);
        }
    }
}
</script>
<style lang="scss" scoped>

</style>
