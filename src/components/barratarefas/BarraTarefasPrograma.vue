<template>
    <div class="barratarefas-programa" v-on:click="minimizarJanela">
        <span 
            class="icone"
            :style="{
                backgroundImage: 'url(' + require('@/assets/icon/' + arquivoIcone + '.png') + ')'
            }"
            >
        </span>
        <span class="titulo">{{ arquivoNome }}</span>
    </div>
</template>
<script>
export default {
    name: 'paginaBarraTarefasPrograma',
    props: {
        arquivoNome: String,
        arquivoIcone: String
    },
    methods: {
        minimizarJanela() {
            this.$emit("minimizarJanela", this.arquivoNome)
        }
    }
}
</script>
<style lang="scss" scoped>
.barratarefas-programa {
    cursor: pointer;
    user-select: none;
    text-overflow: ellipsis;
    padding: 2px 4px;
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: flex-start;
    min-width: 60px;
    width: 100%;
    max-width: 160px;
    border-style: solid;
    border-width: 1px;
    border-color: rgb(254, 254, 254) rgb(10, 10, 10) 
     rgb(10, 10, 10) rgb(254, 254, 254);
    box-shadow: rgb(223 223 223) 1px 1px 0px 0px inset,
       rgb(132 133 132) 0px 0px 0px 1px inset;
    background: rgb(198, 198, 198);
    &.active {
        border-style: solid;
        border-width: 1px;
        border-color: rgb(10, 10, 10) rgb(254, 254, 254) 
        rgb(254, 254, 254)rgb(10, 10, 10);
      box-shadow: rgb(233, 233, 233) 1px 1px 0px 0px inset;
    }
    .icone {
        width: 16px;
        height: 16px;
        margin-right: 4px;
        background-size: 16px 16px;
        position: relative;
        display: block;
    }
    .titulo {
        white-space: nowrap;
        overflow: hidden;
        text-overflow: ellipsis;
    }
}
</style>