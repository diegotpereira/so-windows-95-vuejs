<template>
    <div class="programa" @dblclick.stop="abrirPrograma">
        <!-- <span class="icone" :style="{ backgroundImage: 'url(' + require('@/assets/icon/' + arquivoIcone + '.png') + ')', }"></span> -->
        <span class="titulo"></span>
    </div>
</template>
<script>
export default {
    name: 'paginaPrograma',
    props: {
        arquiivoNome: String,
        arquivoIcone: String
    },
    methods: {
        abrirPrograma() {
            this.$emit("abriPrograma", this.arquiivoNome, this.arquivoIcone)
        }
    }
}
</script>
<style lang="scss" scoped>
.programa {
    height: 75px;
    width: 86px;
    display: flex;
    flex-direction: column;
    align-items: center;
}
</style>