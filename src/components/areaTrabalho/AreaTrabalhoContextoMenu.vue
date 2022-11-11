<template>
    <div class="areatrabalhocontextomenu">
        <div class="link"><span>Organizar ícones</span><span>></span></div>
        <div class="link"><span>Ícones de alinhamento</span></div>
        <div class="link"></div>
        <div class="link"></div>
        <div class="divisor"></div>
        <div class="link">Propriedades</div>
    </div>
</template>
<script>
export default {
    name: 'paginaAreaTrabalhoContexto',
    data() {
        return {
            
        }
    },
    props: {
        posicao: Array
    }
}
</script>
<style lang="scss" scoped>
.areatrabalhocontextomenu {
    @include v95();
    position: absolute;
    min-width: 122px;
    padding: 2px;
    z-index: 10;
    user-select: none;
    .link {
        display: flex;
        align-items: center;
        justify-content: space-between;
        cursor: pointer;
        height: 24px;
        padding: 4px 8px 4px 16px;
        &:hover {
            background-color: $highlightV95;
            color: white;
        }
        span {
            &:nth-of-type(2) {
                font-weight: bold;
            }
        }
    }
    .divisor {
        margin-right: 4px;
        border-style: solid;
        border-width: 1px;
        border-color: rgb(254, 254, 254) rgb(223 223 223) rgb(254, 254, 254)
      rgb(254, 254, 254);
    }
}
</style>