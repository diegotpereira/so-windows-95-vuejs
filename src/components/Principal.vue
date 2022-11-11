<template>
    <div 
        class="container" 
        :class="{ 
            modoTelaCheia: modoTelaCheia, 
            Modocrt: Modocrt }">
        <div>
            <AreaTrabalho
               :programas="programas"
               :programasAberto="programasAberto"
               @abrirPrograma="abrirPrograma"
               @fecharPrograma="fecharPrograma"
               @Modocrt="alternarModoCrt" 
               @modoTelaCheia="alternarModoTelaCheia"
               @redefinirDesktopContexto="redefinirDesktopContexto"
               @minimizarJanela="minimizarJanela" 
            />

            <BarraTarefas 
                :programas="programas"
                :programasAberto="programasAberto"
                :desktopIniciarMenuAtivo="desktopIniciarMenuAtivo"
                @abrirPrograma="abrirPrograma"
                @alternarBarraTarefas="alternarBarraTarefas"
                @fecharBarraTarefas="fecharBarraTarefas"
                @minimizarJanela="minimizarJanela"
            />
        </div>
    </div>
</template>
<script>
import AreaTrabalho from './areaTrabalho/AreaTrabalho.vue'
import Diretorio from '../data/Diretorio.vue'
import BarraTarefas from './barratarefas/BarraTarefas.vue'

export default {
    name: 'paginaPrincipal',
    data() {
        return {
            modoTelaCheia: false,
            programasAberto: [],
            programas: Diretorio,
            Modocrt: true,
            desktopIniciarMenuAtivo: false
        }
    },
    components: {
        AreaTrabalho,
        BarraTarefas
    },
    methods: {
        abrirPrograma(arquivoNome, arquivoIcone, arquivoTipo, arquivos) {

            if (this.programasAberto.find(([titulo]) => titulo === arquivoNome)) {
                
                console.log("encontrado");

            } else {
                this.programasAberto.push([arquivoNome, arquivoIcone, arquivoTipo, arquivos])
            }
        },
        alternarBarraTarefas() {
            this.desktopIniciarMenuAtivo != this.desktopIniciarMenuAtivo;
        },
        redefinirDeskTopContexto() {
            this.desktopIniciarMenuAtivo = false;
        },
        alternarModoCrt() {
            this.Modocrt != this.Modocrt;
        },
        alternarModoTelaCheia() {
            this.modoTelaCheia != this.modoTelaCheia;
        },
        fecharBarraTarefas() {
            this.desktopIniciarMenuAtivo = false
        },
        minimizarJanela(arquivoNome) {

            for(let i = 0; i < this.programasAberto.length; i++) {
                if(this.programasAberto[i][0] == arquivoNome) {
                    this.programasAberto[i][3] = !this.programasAberto[i][3];
                }
            }
        },
        fecharPrograma(arquivoNome) {
            console.log("Aqui");
            for(let i = 0; i < this.programasAberto.length; i++) {
                if(this.programasAberto[i][0] == arquivoNome) 
                   this.programasAberto.splice(i, 1);
            }
        },
        redefinirDesktopContexto() {
            this.desktopIniciarMenuAtivo = false;
        }
    }
}
</script>
<style lang="scss" scoped>

@keyframes flicker {
    0% {
        opacity: 0.27861;
    }
    5% {
    opacity: 0.34769;
    }
    10% {
        opacity: 0.23604;
    }
    15% {
        opacity: 0.90626;
    }
    20% {
        opacity: 0.18128;
    }
    25% {
        opacity: 0.83891;
    }
    30% {
        opacity: 0.65583;
    }
    35% {
        opacity: 0.67807;
    }
    40% {
        opacity: 0.26559;
    }
    45% {
        opacity: 0.84693;
    }
    50% {
        opacity: 0.96019;
    }
    55% {
        opacity: 0.08594;
    }
    60% {
        opacity: 0.20313;
    }
    65% {
        opacity: 0.71988;
    }
    70% {
        opacity: 0.53455;
    }
    75% {
        opacity: 0.37288;
    }
    80% {
        opacity: 0.71428;
    }
    85% {
        opacity: 0.70419;
    }
    90% {
        opacity: 0.7003;
    }
    95% {
        opacity: 0.36108;
    }
    100% {
        opacity: 0.24387;
    }
}
.container {
    width: 100%;
    max-width: 640px;
    height: 480px;
    position: relative;
    overflow: hidden;

    &.Modocrt {
        &:after {
            content: " ";
            display: block;
            top: 0;
            left: 0;
            bottom: 0;
            right: 0;
            background: rgba(18, 16, 16, 0.1);
            opacity: 0;
            z-index: 100;
            pointer-events: none;
            animation: flicker 0.15s infinite;
        }
    }
    &.modoTelaCheia {
        max-width: 100%;
        height: 100%;
        .areatrabalho {
            height: 100% !important;
        }
    }
}

</style>