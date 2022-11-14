<template>
    <div class="aol">
        <div>
            <div>
                <span class="titulo">erro crítico</span>
                <span>
                    Ocorreu uma exceção fatal 0x1337 em ./aol-wrapper.vb:1337 em
                    "AOL.exe". O aplicativo atual será encerrado.
                </span>
                <span>
                    <br />pressione qualquer tecla para continuar
                    <span>_</span>
                </span>
            </div>
        </div>
    </div>
</template>
<script>
export default {
    name: 'paginaAol',
    props: {
        arquivoNome: String
    },
    methods: {
        fecharPrograma(arquivoNome) {
            this.$emit("fecharPrograma", arquivoNome)
        }
    },
    mounted() {
        window.addEventListener("keypress", function(e) {
            this.fecharPrograma(this.arquivoNome, e);
        }.bind(this));
    }
}
</script>
<style lang="scss" scoped>
.aol {
    position: fixed;
    display: flex;
    justify-content: space-around;
    align-items: center;
    position: fixed;
    left: 0;
    top: 0;
    width: 100%;
    height: 100%;
    > div {
        background: blue;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        position: fixed;
        min-width: 640px;
        min-height: 480px;
        color: white;
        font-size: 16px;
        line-height: 20px;
        > div {
            background: blue;
            display: flex;
            flex-direction: column;
            text-align: left;
            max-width: 350px;
            span.titulo {
                color: blue;
                margin-bottom: 20px;
                background: white;
            }
            span span {
                animation: cursor-blink 1.5s steps(2) infinite;
            }
        }
    }
    @keyframes cursor-blink {
        0% {
            opacity: 0;
        }
    }
}
</style>