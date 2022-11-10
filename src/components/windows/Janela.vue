<template>
    <div class="janela">
        <div class="menu-bar">
            <div class="titulo">
                <!-- <span class="icone" :style="{backgroundImage: 'url(' + require('@/assets/icon/' + arquivoIcone + '.png') + ')', }"></span> -->

            </div>
            <div class="acoes">
                <div>
                    <img src="" alt="">
                </div>
                <div>
                    <img src="" alt="">
                </div>
                <div>
                    <img src="" alt="">
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