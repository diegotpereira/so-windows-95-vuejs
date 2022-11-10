<template>
    <div class="areatrabalho">
        <div class="programas">
            <Janela>

            </Janela>
            <Programa>
                
            </Programa>
        </div>
    </div>
</template>
<script>
import Janela from '../windows/Janela.vue'
import Programa from './programas/Programa.vue'

export default {
    name: 'paginaAreaTrabalho',
    components: {
        Janela,
        Programa
    }
}
</script>