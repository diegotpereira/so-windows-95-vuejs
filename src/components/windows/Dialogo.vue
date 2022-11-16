<template>
    <div class="dialogo">
        <div class="dialogo-janela">
            <div class="menu-bar">
                <div class="titulo">
                    <span 
                        class="icone"
                        :style="{
                            backgroundImage: 
                                'url(' + require('@/assets/icon/Warning.png') + ')',
                        }">

                    </span>
                    <span>Alerta</span>
                </div>
                <div class="acoes">
                    <div>
                        <img :src="require('@/assets/icon/minimize.png')" alt="">
                    </div>
                    <div>
                        <img :src="require('@/assets/icon/maximize.png')" alt="">
                    </div>
                    <div>
                        <img :src="require('@/assets/icon/close.png')" alt="">
                    </div>
                </div>
            </div>
            <div class="dialogo-corpo">
                <div class="conteudo">
                    <img src="" alt="">
                </div>
                <div class="botao">OK</div>
            </div>
        </div>
    </div>
</template>
<script>
export default {
    name: 'paginaDialogo',
    props: {
        arquivoNome: String 
    },
    methods: {
        fecharPrograma(arquivoNome) {
            this.$emit("fecharPrograma", arquivoNome);
        }
    }
}
</script>
<style lang="scss" scoped>
.dialogo {
    position: fixed;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;
    z-index: 20;
    display: flex;
    align-items: center;
    justify-content: center;
    user-select: none;
    &:before {
        content: "";
        position: absolute;
        top: 0;
        right: 0;
        bottom: 0;
        left: 0;
    }
    .menu-bar {
        height: 18px;
        display: flex;
        flex-direction: row;
        align-items: center;
        justify-content: space-between;
        background-color: $highlightV95;
        padding: 0px 3px;
        .titulo {
            padding: 2px 0px;
            display: flex;
            flex-direction: row;
            align-items: center;
            color: white;
            .icone {
                width: 14px;
                height: 14px;
                margin-right: 4px;
                background-size: 14px 14px;
                position: relative;
                margin-bottom: 2px;
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
                border-color: rgb(254, 254, 254) rgb(10, 10, 10)
                                rgb(10, 10, 10) rgb(254, 254, 254);
                box-shadow: rgb(223 , 223, 223) 1px 1px 0px 0px inset;
                img {
                    -webkit-filter: invert(40%);
                    filter: invert(40%);
                }
            }
        }
    }
    .dialogo-janela {
        width: 300px;
        height: 105px;
        padding: 2px;
        position: relative;
        z-index: 21;
        background-color: rgba(191, 193, 192, 1);
        border-style: solid;
        border-color: rgb(254, 254, 254) rgb(10, 10, 10)
                        rgb(10, 10, 10) rgb(254, 254, 254);
        box-shadow: rgb(223, 223, 223) 1px 1px 0px 0px inset,
                      rgb(132, 133, 132) 0px 0px 0px 1px inset;
        .dialogo-corpo {
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            width: 100%;
            .conteudo {
                display: flex;
                flex-direction: row;
                align-items: center;
                justify-content: flex-start;
                width: 100%;
                text-align: center;
                height: 40px;
                div {
                    margin-left: 16px;
                }
            }
            .botao {
                @include v95;
                width: 90px;
                text-align: center;
                 padding: 4px;
                margin: 4px;
                pointer-events: auto;
                &:active,
                &:focus {
                @include v95Hover;
                }
            }
        }
    }
}
</style>