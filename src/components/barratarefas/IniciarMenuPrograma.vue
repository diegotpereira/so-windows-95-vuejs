<template>
    <div class="iniciar-menu-programa" v-on:click="abrirPrograma">
        <span 
            class="icone"
            :style="{
                backgroundImage: 
                'url(' + require('@/assets/icon/' + arquivoIcone + '.png') + ')',
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
.iniciar-menu-programa {
    cursor: pointer;
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: flex-start;
    height: 32px;
    padding: 0px 6px;
    &:hover,
    &:active {
        background-color: $highlightV95;
        color: white;
    }
    .icone {
        width: 24px;
        min-width: 24px;
        height: 24px;
        margin-right: 8px;
        background-size: 24px 24px;
        position: relative;
        display: block;
    }
}
</style>
