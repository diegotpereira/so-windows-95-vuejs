<template>
    <div class="barratarefas">
        <div class="intro">
            <div class="involucro-menu-iniciar" ref="iniciarmenu">
                <div class="iniciar-menu" v-if="this.desktopIniciarMenuAtivo">
                    <div>
                        <span>Windows<span>95</span></span>
                    </div>
                    <div class="involucro-menu-programa-iniciar">
                        <IniciarMenuPrograma 
                            href="www.google.com"
                            :arquivoNome="'GitHub'"
                            :arquivoIcone="'GitHub'"
                        />
                        <div class="divisor"></div>
                        <IniciarMenuPrograma 
                            v-for="(programa, index) in programas.slice(0, 6)" 
                            v-bind:key="index"
                            :arquivoNome="programa[0]"
                            :arquivoIcone="programa[1]"
                            :arquivoTipo="programa[2]"
                            :arquivos="programa[4]"
                            @abrirPrograma="abrirPrograma"
                        />
                        <div class="divisor"></div>
                        <IniciarMenuPrograma 
                            :arquivoNome="'Desligar...'"
                            :arquivoIcone="'Shutdown'"
                        />
                    </div>
                </div>
                <div class="iniciar" v-on:click="alternarBarraTarefas">
                    <div 
                       class="icone"
                       :style="{ 
                        backgroundImage: 'url(' + require('@/assets/icon/start.png') + ')',}"
                        >
                    </div>
                    Iniciar
                </div>
            </div>
            <div class="divisor"></div>
            <div class="barratarefas-programa-involucro">
                <BarraTarefasPrograma 
                    v-for="(programa, index) in programasAberto" 
                    v-bind:key="index"
                    :arquivoNome="programa[0]"
                    :arquivoIcone="programa[1]"
                    @minimizarJanela="minimizarJanela"
                    @abrirPrograma="abrirPrograma"
                />
            </div>
            <div class="divisor"></div>
            <Relogio />
        </div>
    </div>
</template>
<script>
import Relogio from './Relogio.vue'
import IniciarMenuPrograma from './IniciarMenuPrograma.vue'
import BarraTarefasPrograma from './BarraTarefasPrograma.vue'

export default {
    name: 'paginaBarraTarefas',
    data() {
        return {
        }
    },
    props: {
        desktopIniciarMenuAtivo: Boolean,
        programas: Object,
        programasAberto: Object
    },
    components: {
        Relogio,
        IniciarMenuPrograma,
        BarraTarefasPrograma
    },
    methods: {
        alternarBarraTarefas() {
            this.$emit("alternarBarraTarefas");
        },
        abrirPrograma(arquivoNome, arquivoIcone, arquivoTipo, arquivos) {
            this.$emit("abrirPrograma", arquivoNome, arquivoIcone, arquivoTipo, arquivos);
            this.$emit("fecharBarraTarefas");
        },
        minimizarJanela(arquivoNome) {
            this.$emit("minimizarJanela", arquivoNome);
            this.$emit("fecharBarraTarefas");
        },
        fecharBarraTarefas() {
            this.$emit("fecharBarraTarefas");
        }
    },
}
</script>

<style lang="scss" scoped>
.barratarefas {
    @include v95;
    padding: 2px 3px;
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: space-between;
    height: 29px;
    z-index: 5;
    .intro {
        display: flex;
        flex-direction: row;
        align-items: stretch;
        justify-content: flex-start;
        white-space: nowrap;
        height: 100%;
        width: 100%;
        .involucro-menu-iniciar {
            position: relative;
            user-select: none;
            .iniciar {
                @include v95;
                cursor: pointer;
                display: flex;
                align-items: center;
                justify-content: center;
                margin-right: 4px;
                padding: 2px 4px;
                font-weight: bold;
                height: 100%;
                &:active {
                    border-style: solid;
                    border-width: 1px;
                    border-color: rgb(10, 10, 10) rgb(254, 254, 254) rgb(254, 254, 254)
                        rgb(10, 10, 10);
                    box-shadow: rgb(223 223 223) 1px 1px 0px 0px inset;
                }
                .icone {
                    width: 16px;
                    height: 16px;
                    margin-right: 4px;
                    background-size: 16px 16px;
                    position: relative;
                    display: block;
                }
            }
            .iniciar-menu {
                @include v95();
                display: flex;
                flex-direction: row;
                align-items: flex-start;
                justify-content: flex-start;
                position: absolute;
                bottom: calc(100% + 3px);
                left: -4px;
                width: 164px;
                height: 275px;
                z-index: 2;
                padding: 2px 3px 3px 2px;
                > div {
                    &:nth-of-type(1) {
                        display: flex;
                        align-items: flex-end;
                        justify-content: center;
                        margin-right: 3px;
                        background-color: #808080;
                        height: 100%;
                        width: 24px;
                        > span {
                            opacity: 0.8;
                            display: block;
                            transform: rotate(270deg);
                            margin-bottom: 48px;
                            margin-left: 1px;
                            font-weight: 600;
                            color: #c0c0c0;
                            font-size: 22px;
                            span {
                                padding-left: 2px;
                                font-weight: 300;
                                color: white;
                            }
                        }
                    }
                    &:nth-of-type(2) {
                        width: 100%;
                    }
                }
            }
            .involucro-menu-programa-iniciar {
                .divisor {
                    margin: 2px 2px 2px 0px;
                    border-style: solid;
                    border-width: 1px;
                    border-color: rgb(254, 254, 254) rgb(223, 223, 223) rgb(254, 254, 254)
                                    rgb(254, 254, 254);
                }
            }
        }
    }
    .divisor {
        margin-right: 4px;
        border-style: solid;
        border-width: 1px;
        border-color: rgb(254, 254, 254) rgb(223, 223, 223)
                        rgb(254, 254, 254) rgb(254, 254, 254);
    }
    .barratarefas-programa-involucro {
        display: flex;
        flex-direction: row;
        align-items: flex-start;
        justify-content: flex-start;
        overflow: hidden;
        width: 100%;
    }
}
.relogio {
    margin-right: 2px;
    padding: 2px 4px;
    background-color: rgba(191, 193, 192, 1);
    border-style: solid;
    border-width: 1px;
    border-color: rgb(254, 254, 254) rgb(10, 10, 10)
                    rgb(10, 10, 10) rgb(132, 133, 132) 0px 0px 0px 1px inset;
    box-shadow: rgb(223 223 223) 1px 1px 0px 0px inset,
                rgb(132 133 132) 0px 0px 0px 1px inset;
}
</style>