<template>
    <div id="banner">
        <div class="container fluid">
            <h1 class="site-title">Mujer Real</h1> 
            <h3 class="site-title"> Para mujeres reales como tú y como yo</h3><br>
            <div align="center"><img src="@/assets/banner.png" alt="Banner de la tienda de Ropa" width="800" height="450"></div> <br>
        </div>
        <table id="navBar">
            <tr>
                <th><a><router-link to="/">Inicio</router-link></a></th>
                <th><a><router-link to="/productos">Productos</router-link></a></th>
                <th><a><router-link to="/clientes">Clientes</router-link></a></th>
                <th><a><router-link to="/carrito">Carrito</router-link></a></th>
            </tr>
        </table>
    </div>
</template>
<script>
export default {
    name: 'menu'
}
</script>
<style scoped>
    .titulos {
        font-family: verdana;
        font-size: 60px;
    }
    #banner {
        background-color: #edecec;
    }
</style>
