<template>
    <div 
       class="areatrabalho"
       ref="areatrabalho">
        <div class="programas">
            <Janela
               v-for="(programa, index) in programasAberto" 
               v-bind:key="index"
               :arquivoNome="programa[0]"
               :arquivoIcone="programa[1]"
               :arquivoTipo="programa[2]"
               :arquivos="[4]"
               :programasAberto="programasAberto"
               @abrirPrograma="abrirPrograma">
               <component :is="programa[1]"></component>
            </Janela>
            <Programa 
               v-for="(programa, index) in programas" 
               v-bind:key="index"
               :arquivoNome="programa[0]"
               :arquivoIcone="programa[1]"
               :arquivoTipo="programa[2]"
               :arquivos="[4]"
               @abrirPrograma="abrirPrograma">
            </Programa>
            <AreaTrabalhoContextoMenu 
               v-if="this.desktopMenuContextoAtivo"
               :posicao="this.desktopMenuContextoPosicao"
               @modoTelaCheia="$emit('modoTelaCheia')"
               @Modocrt="$emit('Modocrt')">
            </AreaTrabalhoContextoMenu>
        </div>
    </div>
</template>
<script>
// import Janela from '../windows/Janela.vue'
import Programa from './programas/Programa.vue'
import AreaTrabalhoContextoMenu from './AreaTrabalhoContextoMenu.vue'

export default {
    name: 'paginaAreaTrabalho',
    data() {
        return {
            desktopMenuContextoAtivo: false,
            desktopMenuContextoPosicao: [0, 0]
        }
    },
    components: {
        // Janela,
        Programa,
        AreaTrabalhoContextoMenu
    },
    props: {
        programas: Object,
        programasAberto: Object
    },
    methods: {
        abrirPrograma(arquivoNome, arquivoIcone, arquivoTipo, arquivos) {
            this.$emit("abrirPrograma", arquivoNome, arquivoIcone, arquivoTipo, arquivos);
        },
        desktopContextoMenu(e) {
            e.preventDefault();
            e.stopPropagation();
            this.desktopMenuContextoPosicao[0] = 
               e.pageX - this.$refs.areatrabalho.getBoundingClientRect().left;

            this.desktopMenuContextoPosicao[1] = 
               e.pageY -  this.$refs.areatrabalho.getBoundingClientRect().top;

            this.desktopMenuContextoAtivo = true;
        }
    }
}
</script>
<style lang="scss" scoped>
.areatrabalho {
    width: 100%;
    height: 452px;
    padding: 0;
    position: relative;
    background-color: #008080;
    .programas {
        height: 100%;
        display: flex;
        flex-direction: column;
        flex-wrap: wrap;
        justify-content: flex-start;
        align-items: flex-start;
        align-content: flex-start;
    }
}
</style>