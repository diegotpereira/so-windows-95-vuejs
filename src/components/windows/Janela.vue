<template>
    <div 
        class="janela"
        v-if="minimizar"
        style="z-index: 2"
        @mousedown="JanelaMouseBaixo($event)"
        v-on:click.right.stop="preventDefault($event)"
        :class="{ maximizar: maximizarJanela }">
        <div 
            class="menu-bar"
            @dblclick.stop="duploClique($event)"
            @mousedown="mouseParaBaixo($event)"
            @mouseup="mouseParaCima()"
            @mousemove="mouseMover($event)"
            @mouseleave="mouseFolha($event)">
            <div 
                class="titulo">
                <span 
                    class="icone" 
                    :style="{
                        backgroundImage: 
                            'url(' + require('@/assets/icon/' + arquivoIcone + '.png') + ')', }">
                </span>
                <span>{{ arquivoNome }}</span>
            </div>
            <div class="acoes">
                <div v-on:click="minimizarJanela()" @mouseleave="liberarJanela()">
                    <img :src="require('@/assets/icon/minimize.png')" alt="">
                </div>
                <div v-on:click="maximizar()" @mouseleave="liberarJanela()">
                    <img :src="require('@/assets/icon/maximize.png')" alt="">
                </div>
                <div v-on:click="fecharPrograma" @mouseleave="liberarJanela()">
                    <img :src="require('@/assets/icon/close.png')" alt="">
                </div>
            </div>
        </div>
        <div class="carregar-programa">
            <component 
                :is="carregarPrograma"
                :arquivoNome="arquivoNome"
                :arquivoIcone="arquivoIcone"
                :arquivoTipo="arquivoTipo"
                :programasAberto="programasAberto"
                @abrirPrograma="abrirPrograma"
                @fecharPrograma="fecharPrograma"
                >
            </component>
        </div>
    </div>
</template>
<script>
import Internet from './Internet.vue'
import Pasta from './Pasta.vue'
import Dialogo from './Dialogo.vue'
import BlocoNotas from './/BlocoNotas.vue'
import Paint from './Paint.vue'
import AOL from './AOL.vue'

export default {
    name: 'paginaJanela',
    data() {
        return {
            carregarPrograma: this.arquivoTipo,
            ponto: {
                state: "up",
                xDiff: 0,
                yDiff: 0
            },
            maximizarJanela: false
        }
    },
    props: {
        arquivoNome: String,
        arquivoIcone: String,
        arquivoTipo: String,
        programasAberto: Array,
        minimizar: Boolean
    },
     components: {
        Internet,
        Pasta,
        Dialogo,
        BlocoNotas,
        Paint,
        AOL
    },
    mounted: function() {
        this.zCiclo();
    },
    methods: {
        abrirPrograma(arquivoNome, arquivoIcone, arquivoTipo, arquivos) {
            this.$emit("abrirPrograma", arquivoNome, arquivoIcone, arquivoTipo, arquivos);
        },
        fecharPrograma() {
            this.$emit("fecharPrograma", this.arquivoNome);
        },
        zCiclo(zIndice) {

            var programas = document.querySelectorAll(".janela");
            zIndice = zIndice || 2;

            for(let i = 0; i < programas.length; i++) {
                if (parseInt(programas[i].style.zIndice) > zIndice) {
                    programas[i].style.zIndice = parseInt(programas[i].style.zIndice) - 1;
                }
            }
        },
        JanelaMouseBaixo(event) {
            let elemento = event.target;
            let maxIndice = document.querySelectorAll(".janela").length;
            this.zCiclo(parseInt(elemento.style.zIndice));
            elemento.style.zIndice = maxIndice + 2;
        },
        duploClique(event) {
            this.maximizarJanela = !this.maximizarJanela;
            event.preventDefault();
        },
        mouseParaBaixo(event) {
            let elemento = event.target.parentNode;
            this.ponto.state = "down";

            if(this.ponto.yDiff == 0)
               this.ponto.yDiff = elemento.offsetTop - event.clientY;

            if(this.ponto.xDiff == 0)
               this.ponto.xDiff = elemento.offsetLeft - event.clientX;

            let maxIndice = document.querySelectorAll(".janela").length;
            this.zCiclo(parseInt(elemento.style.zIndice));
            elemento.style.zIndice = maxIndice + 2;
        },
        mouseMover(event) {
            if (this.ponto.state == "down") {
                let elemento = event.target.parentNode;

                elemento.style.top = this.ponto.yDiff + event.clientY + "px";
                elemento.style.left = this.ponto.xDiff + event.clientX + "px";
            }
        },
        mouseFolha(event) {
            if (this.ponto.state  == "down") {
                this.mouseMover(event);
            } else {
                this.liberarJanela();
            }
        },
        mouseParaCima() {
            this.liberarJanela();
        },
        liberarJanela() {
            this.ponto.state = "up";
            this.ponto.xDiff = 0;
            this.ponto.yDiff = 0;
        },
        minimizarJanela() {
            this.$emit("minimizarJanela", this.arquivoNome);
        },
        maximizar() {
            this.maximizarJanela = !this.maximizarJanela;
        },
        preventDefault(event) {
            event.stopPropagation();
            event.preventDefault();
        }
    },
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
                  rgb(132, 133, 132) 0px 0px 0px 1px inset;
    &.maximizar {
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
        align-items: center;
        justify-content: space-between;
        background-color: $highlightV95;
        padding: 0px 3px;
        user-select: none;
        .titulo {
            padding: 2px 0px;
            display: flex;
            flex-direction: row;
            align-items: center;
            color: white;
            pointer-events: none;
            .icone {
                width: 16px;
                height: 16px;
                margin-right: 2px;
                background-size: 16px 16px;
                position: relative;
                display: block;
            }
        }
        .acoes {
            display: flex;
            flex-direction: row;
            align-items: center;
            justify-content: flex-end;
            div {
                width: 16px;
                height: 14px;
                display: flex;
                align-items: center;
                justify-content: center;
                background-color: rgba(191, 193, 192, 1);
                border-style: solid;
                border-width: 1px;
                border-color: rgb(254, 254, 254) rgb(10, 10, 10)
                                rgb(10, 10, 10) rgb(254, 254, 254);

                box-shadow: rgb(223 223 223) 1px 1px 0px 0px inset;
                &:active {
                    border-style: solid;
                    border-width: 1px;
                    border-color: rgb(10, 10, 10) rgb(254, 254, 254) 
                                  rgb(254, 254, 254) rgb(10, 10, 10);
                box-shadow: rgb(223 223 223) 1px 1px 0px 0px inset;

                }
            }
        }
    }
    .carregar-programa {
        overflow: auto;
        height: 100%;
        width: 100%;
        > div {
            height: 100%;
            width: 100%;
        }
    }
}
</style>