<template>
    <div class="pasta">
        <div class="arquivo-explorar">
            <Programa 
                v-for="(arquivo, index) in diretorioAtual" 
                v-bind:key="index"
                :arquivoNome="arquivo[0]"
                :arquivoIcone="arquivo[1]"
                :arquivoTipo="arquivo[2]"
                :arquivos="arquivo[4]"
                :programasAberto="programasAberto"
                @abrirPrograma="abrirPrograma"
            />
        </div>
        <div class="detalhes-bar">
            <div>
                {{ this.diretorioAtual ? this.diretorioAtual.length : "0"}}
                objetos(s)
            </div>
        </div>
    </div>
</template>
<script>
import Programa from '../areaTrabalho/programas/Programa.vue'
export default {
    name: 'paginaPasta',
    data() {
        return {
            diretorioAtual: []
        }
    },
    components: {
        Programa
    },
    props: {
        arquivoNome: String,
        arquivoIcone: String,
        arquivoTipo: String,
        arquivos: Array,
        programasAberto: Array,
    },
    created() {
        this.carregarDiretorio(this.programasAberto, this.arquivoNome)
    },
    methods: {
        carregarDiretorio(buscarDiretorio, arquivoBuscar) {

            let resultadoFiltrado = buscarDiretorio
               .filter((linha) => linha[0] === arquivoBuscar)
               .map((linha) => linha);
            this.diretorioAtual = resultadoFiltrado[0][4];
        },
        abrirPrograma(arquivoNome, arquivoIcone, arquivoTipo, arquivos) {
            this.$emit("abrirPrograma", arquivoNome, arquivoIcone, arquivoTipo, arquivos);
        }
    }
}
</script>
<style lang="scss" scoped>
.pasta {
    height: 100%;
    width: 100%;
    overflow: auto;
    display: flex;
    flex-direction: column;
    .arquivos-bar {
        @include v95Hover;
        background-color: rgba(191, 193, 192, 1);
        padding: 4px 2px 2px 2px;
        margin-top: 2px;
        display: flex;
        flex-direction: row;
        align-items: center;
        justify-content: flex-start;
        user-select: none;
    }
    .detalhes-bar {
        @include v95Hover;
        background-color: rgba(191, 193, 192, 1);
        padding: 4px 2px 2px 2px;
        margin-top: 2px;
        display: flex;
        flex-direction: row;
        align-items: center;
        justify-content: flex-start;
        user-select: none;
    }
    .arquivo-explorar {
        width: 100%;
        height: 100%;
        display: flex;
        flex-direction: row;
        flex-wrap: wrap;
        justify-content: flex-start;
        align-items: flex-start;
        align-content: flex-start;
        overflow: auto;
        @include v95Hover;
        background-color: white;
    }
}
</style>