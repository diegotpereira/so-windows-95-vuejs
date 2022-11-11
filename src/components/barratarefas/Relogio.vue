<template>
    <div class="barratarefas-relogio">
        <div 
           class="barratarefas-audio"
           :style="{ backgroundImage: 'url(' + require('@/assets/icon/Volume.png') + ')',}">

        </div>
        <div>{{ this.atualHora }}</div>
    </div>
</template>
<script>
export default {
    name: 'paginaRelogio',
    data() {
        return {
            atualHora: new Date().toLocaleTimeString([], { timeStyle: "short"})
        }
    },
}
</script>
<style lang="scss" scoped>
.barratarefas-relogio {
    display: flex;
    flex-direction: row;
    align-items: center;
    position: relative;
    white-space: nowrap;
    user-select: none;
    padding: 2px 4px;
    border-style: solid;
    border-width: 1px;
    border-color: rgb(10, 10, 10) rgb(254, 254, 254) 
                  rgb(254, 254, 254)rgb(10, 10, 10);
    box-shadow: rgb(223, 223, 223) 1px 1px 0px 0px inset;
    .barratarefas-audio {
        width: 16px;
        height: 16px;
        margin-right: 4px;
        background-size: 16px 16px;
        position: relative;
        display: block;
    }
}
</style>