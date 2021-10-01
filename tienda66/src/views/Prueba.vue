<template>
    <div class="container">
        <h1>Mi prueba de rutas</h1>
        <MiComponente/>
    </div>
</template>
<script>
import MiComponente from '@/components/MiComponente.vue'

export default {
    components: {
        MiComponente
        
    },
    created (){
        console.log('Holaa')
    }
}
</script>