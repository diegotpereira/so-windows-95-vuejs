<template>
    <div class="container">
        <div>
            <AreaTrabalho
               :programasAberto="programasAberto"
               @abrirPrograma="abrirPrograma" />
        </div>
    </div>
</template>
<script>
import AreaTrabalho from './areaTrabalho/AreaTrabalho.vue'

export default {
    name: 'paginaPrincipal',
    data() {
        return {
            programasAberto: []
        }
    },
    components: {
        AreaTrabalho
    },
    methods: {
        abrirPrograma(arquivoNome, arquivoIcone) {

            if (this.programasAberto.find(([titulo]) => titulo === arquivoNome)) {
                
                console.log("encontrado");

            } else {
                this.programasAberto.push([arquivoNome, arquivoIcone])
            }
        }
    }
}
</script>