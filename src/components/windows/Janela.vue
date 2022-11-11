<template>
    <div class="janela">
        <div class="menu-bar">
            <div class="titulo">
                <span class="icone" :style="{backgroundImage: 'url(' + require('@/assets/icon/' + arquivoIcone + '.png') + ')', }"></span>
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
}
</style>