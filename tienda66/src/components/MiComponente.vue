<template>
    <div class="container">
        <h1>Bienvenido {{ cliente.nombre }}</h1>
        <div class="container">
            <div class="row">
                <input type="text" v-model="cliente.nombre">
                <input type="number" v-model="cantidad">
            </div>
            <div class="row">
                <h3 v-if="cantidad > 0">Número mayor a cero</h3>
                <p v-else-if="cantidad === 0">Número igual a cero</p>
                <h2 v-else>Número negativo</h2>
            </div>
            <div class="row">
                <h2 v-show="cantidad > 0" >Número positivo (con v-show)</h2>
            </div>
        </div>
        <!--
        <div class="container">
            {{ productos }}
        </div>
        -->
        <div class="container">
            <div v-for="producto in productos" :key="producto.id">
                <h1>Producto: {{ producto.nombre}} </h1>
                <h2>Precio: {{producto.precio}} </h2>
                <button type="button" @click="mostrarPrecioAcumulado(producto.precio)">Agregar</button>
            </div>
        </div>
        <div class="container">
            <h3> <b>PRECIO TOTAL = $</b> {{ precioAcumulado }} </h3>
        </div>
    </div>
</template>
<script>
export default {
    data() {
        return {
            cliente: { nombre: 'Natacha', apellido: 'Libreros' },
            cantidad: 0,
            // arreglo:
            productos: [
                // objetos:
                {
                    id: 1,
                    nombre:'camiseta',
                    precio: 25000
                },
                {
                    id: 2,
                    nombre:'vestido',
                    precio: 150000
                },
                {
                    id: 3,
                    nombre:'pantalón',
                    precio: 120000
                }
            ],
            precioAcumulado: 0
        }
    },
    methods: {
        mostrarPrecioAcumulado (precioProducto) {
            // Ejemplo
            let variable1 = 'mi_variable'
            const mi_constante = 5
            console.log(variable1)
            console.log(mi_constante)
            ////
            this.precioAcumulado = this.precioAcumulado + precioProducto
        }
    }
}
</script>