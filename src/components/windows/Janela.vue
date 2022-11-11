<template>
    <div class="janela">
        <div class="menu-bar">
            <div class="titulo">
                <span 
                    class="icone" 
                    :style="{
                        backgroundImage: 
                            'url(' + require('@/assets/icon/' + arquivoIcone + '.png') + ')', }">
                </span>
                <span>{{ arquivoNome }}</span>
            </div>
            <div class="acoes">
                <div>
                    <img :src="('@/assets/icon/minimize.png')" alt="">
                </div>
                <div>
                    <img :src="('@/assets/icon/maximize.png')" alt="">
                </div>
                <div>
                    <img :src="('@/assets/icon/close.png')" alt="">
                </div>
            </div>
        </div>
        <div class="carregar-programa">
            <component :is="carregarPrograma"
                       :arquivoNome="arquivoNome"
                       :arquivoIcone="arquivoIcone"
                       :arquivoTipo="arquivoTipo"
                       :programasAberto="programasAberto"
                       @abrirPrograma="abrirPrograma">

            </component>

        </div>
    </div>
</template>
<script>
export default {
    name: 'paginaJanela',
    data() {
        return {
            carregarPrograma: this.arquivoTipo
        }
    },
    props: {
        arquivoNome: String,
        arquivoIcone: String,
        arquivoTipo: String,
        programasAberto: Array
    },
    methods: {
        abrirPrograma(arquivoIcone) {
            this.$emit("abrirPrograma", arquivoIcone);
        }
    }
}
</script>
<style lang="scss" scoped>
.janela {
    height: 60%;
    width: 60%;
    position: absolute;
    resize: both;
    overflow: auto;
    top: 10%;
    left: 10%;
    min-height: 150px;
    min-width: 310px;
    padding: 2px;
    display: flex;
    flex-direction: column;
    align-items: stretch;
    justify-content: stretch;
    background-color: rgba(191, 193, 192, 1);
    border-style: solid;
    border-width: 1px;
    border-color: rgb(254, 254, 254) rgb(10, 10, 10)
                    rgb(10, 10, 10) rgb(254, 254, 254);
    box-shadow: rgb(223, 223, 223) 1px 1px 0px 0px inset,
                  rgb(132, 132, 132) 0px 0px 0px 1px inset;
    &.maximize {
        left: 0 !important;
        right: 0 !important;
        bottom: 0 !important;
        top: 0 !important;
        resize: none !important;
        width: auto !important;
        height: auto !important;
    }
    .menu-bar {
        height: 18px;
        display: flex;
        flex-direction: row;
        align-content: center;
        justify-content: space-between;
    }
}
</style>