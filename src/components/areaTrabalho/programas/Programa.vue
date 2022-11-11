<template>
    <div class="programa" @dblclick.stop="abrirPrograma">
        <span 
           class="icone" 
           :style="{ 
                backgroundImage: 
                    'url(' + require('@/assets/icon/' + arquivoIcone + '.png') + ')', }">
        </span>
        <span class="titulo">{{ arquivoNome }}</span>
    </div>
</template>
<script>
export default {
    name: 'paginaPrograma',
    props: {
        arquivoNome: String,
        arquivoIcone: String,
        arquivoTipo: String,
        arquivos: Array
    },
    methods: {
        abrirPrograma() {
            this.$emit("abrirPrograma", this.arquivoNome, this.arquivoIcone, this.arquivoTipo, this.arquivos)
        }
    }
}
</script>
<style lang="scss" scoped>
.programa {
    height: 75px;
    width: 86px;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    text-align: center;
    padding: 2px;
    color: white;
    user-select: none;
    .titulo {
        border: 1px solid transparent;
        cursor: default;
    }
    .icone {
        width: 32px;
        height: 32px;
        margin-bottom: 8px;
        background-size: 32px 32px;
        position: relative;
        display: block;
    }
    &.active {
        span.titulo {
            background-color: $highlightV95;
            border: 1px dotted #939393;
        }
        .icone {
            filter: opacity(0.5) drop-shadow(0 0 0 $highlightV95);
        }
    }
}
</style>