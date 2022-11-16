<template>
    <div 
       class="areatrabalho"
       ref="areatrabalho"
       v-on:click.left="redefinirDesktopContextoMenu"
       v-on:click.right="desktopContextoMenu">
        <div class="programas">
            <Janela
               v-for="(programa, index) in programasAberto" 
               v-bind:key="index"
               :arquivoNome="programa[0]"
               :arquivoIcone="programa[1]"
               :arquivoTipo="programa[2]"
               :arquivos="programa[4]"
               :minimizar="programa[3]"
               :programasAberto="programasAberto"
               @abrirPrograma="abrirPrograma"
               @fecharPrograma="fecharPrograma"
               @minimizarJanela="minimizarJanela"
               >
               <component :is="programa[1]"></component>
            </Janela>
            <Programa 
               v-for="(programa, index) in programas" 
               v-bind:key="index"
               :arquivoNome="programa[0]"
               :arquivoIcone="programa[1]"
               :arquivoTipo="programa[2]"
               :arquivos="programa[4]"
               @abrirPrograma="abrirPrograma" 
               />
        </div>
        <AreaTrabalhoContextoMenu 
               v-if="this.desktopMenuContextoAtivo"
               :posicao="this.desktopMenuContextoPosicao"
               @modoTelaCheia="$emit('modoTelaCheia')"
               @Modocrt="$emit('Modocrt')" 
        />
    </div>
</template>
<script>
import Janela from '../windows/Janela.vue'
import Programa from './programas/Programa.vue'
import AreaTrabalhoContextoMenu from './AreaTrabalhoContextoMenu.vue'
import Internet from '../windows/Internet.vue'
import Pasta from '../windows/Pasta.vue'
import BlocoNotas from '../windows/BlocoNotas.vue'

export default {
    name: 'paginaAreaTrabalho',
    data() {
        return {
            desktopMenuContextoAtivo: false,
            desktopMenuContextoPosicao: [0, 0],
            desktopVolumeMenuAtivo: false
        }
    },
    props: {
        programas: Object,
        programasAberto: Object
    },
    components: {
        Janela,
        Programa,
        AreaTrabalhoContextoMenu,
        Internet,
        Pasta,
        BlocoNotas
    },
    methods: {
        abrirPrograma(arquivoNome, arquivoIcone, arquivoTipo, arquivos) {
            this.$emit("abrirPrograma", arquivoNome, arquivoIcone, arquivoTipo, arquivos);
        },
        fecharPrograma(arquivoNome) {
            this.$emit("fecharPrograma", arquivoNome);
        },
        minimizarJanela(arquivoNome) {
            this.$emit("minimizarJanela", arquivoNome);
        },
        desktopContextoMenu(e) {
            e.preventDefault();
            e.stopPropagation();
            this.$emit("redefinirDesktopContexto");
            this.desktopMenuContextoPosicao[0] = 
               e.pageX - this.$refs.areatrabalho.getBoundingClientRect().left;
            this.desktopMenuContextoPosicao[1] = 
               e.pageY - this.$refs.areatrabalho.getBoundingClientRect().top;
            this.desktopMenuContextoAtivo = true;
        },
        redefinirDesktopContextoMenu() {
            this.$emit("redefinirDesktopContexto");
            this.desktopMenuContextoAtivo = false;
            this.desktopVolumeMenuAtivo = false;

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