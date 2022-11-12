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
        }
    }
}
</style>