<!--<template>
    <div id="contenido">
        Productos
    </div>
</template>  -->

<template>

    <div id="contenido">
        <div class="container div-galeria" id="galeria">
            <div class="row fila-productos">
                <div v-for="producto in productos" :key="producto.id" class="col-lg-4 col-md-6 col-sm-6 col-xs-12 tarjeta-producto">
                    <img class="imagen-producto" :src="getPictureProducto(producto.imagen)">
                    <h1 class="nombre-producto">{{producto.nombre}}</h1>
                    <h3 class="precio-producto">${{producto.precio}}</h3>
                    <div class="descripcion-producto">
                        <p>{{producto.descripcion}}</p>
                    </div>
                    <div class="div-cantidad">
                        <input class="input-cantidad" id="camisa_cantidad" type="number" value="0" min="0">
                    </div>
                    <div id="icono" class="div-icono">
                        <i class="las la-cart-arrow-down estilo-icono" @click="agregarAlCarrito(producto)"></i>
                        <p><b>Agregar al carrito</b></p>
                    </div>
                </div>
            </div>
        </div>
        <div id=div_total class="tarjeta-total">
            <h1><b>TOTAL</b></h1>
            <h2 id="total_carrito">${{total_carrito}}</h2>
            <div id="icono" class="div-icono">
                <i class="las la-cart-arrow-down estilo-icono" @click="irCarrito()"></i>
                <p><b>Ir al carrito</b></p>
            </div>
        </div>
    </div>
</template>
<script>
import axios from 'axios'
export default {
    data () {
        return {
            productos: [],
            carrito: [],
            total_carrito: 0
        }
    },
    created () {
        this.cargarProductos();
        /*
        this.productos =  [
               {
                   id: 1,
                   nombre: 'Camiseta',
                   precio: 25000,
                   imagen: 'real.jpg',
                   descripcion: 'Lorem ipsum dolor sit amet, consectetur adipisicing elit. Recusandae, quidem neque. Eius blanditiis similique dolorem?'
               },
               {
                   id: 2,
                   nombre: 'Vestido',
                   precio: 150000,
                   imagen: 'colgada.jpg',
                   descripcion: 'Lorem ipsum dolor sit amet, consectetur adipisicing elit. Recusandae, quidem neque. Eius blanditiis similique dolorem?'
               },
               {
                   id: 3,
                   nombre: 'Pantalón',
                   precio: 100000,
                   imagen: 'doblados.jpg',
                   descripcion: 'Lorem ipsum dolor sit amet, consectetur adipisicing elit. Recusandae, quidem neque. Eius blanditiis similique dolorem?'
               },
               {
                   id: 4,
                   nombre: 'Falda',
                   precio: 120000,
                   imagen: 'estudiante.jpg',
                   descripcion: 'Lorem ipsum dolor sit amet, consectetur adipisicing elit. Recusandae, quidem neque. Eius blanditiis similique dolorem?'
               },
               {
                   id: 5,
                   nombre: 'Camisa',
                   precio: 45000,
                   imagen: 'camisa.jpg',
                   descripcion: 'Lorem ipsum dolor sit amet, consectetur adipisicing elit. Recusandae, quidem neque. Eius blanditiis similique dolorem?'
               }
           ] */
    },
    methods: {
        getPictureProducto (nombre_archivo) {
            /* Función para cargar imágenes dinámicamente */
            var images = require.context('@/assets/productos/', false, /\.jpg$|\.png$/)
            return images('./' + nombre_archivo)
        },
        agregarAlCarrito(producto) {
            this.carrito.push(producto)
            console.log(this.carrito)
            this.total_carrito = this.total_carrito + producto.precio
            this.$swal.fire(
                'Producto agregado',
                'Se ha agregado ' + producto.nombre + ' al carrito de compras',
                'success'
            )
        },
        irCarrito () {
            let ruta = '/carrito/${this.total_carrito}'
            this.$router.push(ruta)
        },
        cargarProductos(){
            axios.get('http://localhost:3000/api/productos')
             //promesa
            .then(response => {
                let status_peticion = response.status
                console.log(status_peticion)
                this.productos = response.data
            })
        }
    }
}
</script> 

<!--     <div class="container div-galeria" id="galeria">
        <div class="row fila-productos">
            <div class="col-lg-4 col-md-6 col-sm-6 col-xs-12 tarjeta-producto">
                <img class="imagen-producto" style="width: 150px; height: 100px;" src="images/camisas.JPG">
                <h1 class="nombre-producto">Camisas</h1>
                <h3 class="precio-producto">$45.000</h3>
                <div class="descripcion-producto">
                    <p>Camisas de diferentes tallas, telas y colores.</p>
                </div>
                <div id="icono" class="div-icono">
                    <i class="las la-cart-arrow-down estilo-icono" onclick="agregarAlCarrito('Camisa', 45000)"></i>
                    <p><b>Agregar al carrito</b></p>
                </div>
            </div>
            <div class="col-lg-4 col-md-6 col-sm-6 col-xs-12 tarjeta-producto">
                <img class="imagen-producto" style="width: 150px; height: 100px;" src="images/pantalon.JPG">
                <h1 class="nombre-producto">Pantalón</h1>
                <h3 class="precio-producto">$100.000</h3>
                <div class="descripcion-producto">
                    <p>Pantalones de diferentes tallas, telas y colores.</p>
                </div>
                <div id="icono" class="div-icono">
                    <i class="las la-cart-arrow-down estilo-icono" onclick="agregarAlCarrito('Pantalón', 100000)"></i>
                    <p><b>Agregar al carrito</b></p>
                </div>
            </div>
            <div class="col-lg-4 col-md-6 col-sm-6 col-xs-12 tarjeta-producto">
                <img class="imagen-producto" style="width: 150px; height: 100px;" src="images/falda.JPG">
                <h1 class="nombre-producto">Falda</h1>
                <h3 class="precio-producto">$120.000</h3>
                <div class="descripcion-producto">
                    <p>Diferentes de acuerdo a tus gustos</p>
                </div>
                <div id="icono" class="div-icono">
                    <i class="las la-cart-arrow-down estilo-icono" onclick="agregarAlCarrito('Falda', 120000)"></i>
                    <p><b>Agregar al carrito</b></p>
                </div>
            </div>
            <div class="col-lg-4 col-md-6 col-sm-6 col-xs-12 tarjeta-producto">
                <img class="imagen-producto" style="width: 150px; height: 100px;" src="images/vestido.JPG">
                <h1 class="nombre-producto">Vestido</h1>
                <h3 class="precio-producto">$150.000</h3>
                <div class="descripcion-producto">
                    <p>Vestidos largos, a la rodilla y cortos.</p>
                </div>
                <div id="icono" class="div-icono">
                    <i class="las la-cart-arrow-down estilo-icono" onclick="agregarAlCarrito('Vestido', 150000)"></i>
                    <p><b>Agregar al carrito</b></p>
                </div>
            </div>
            <div class="col-lg-4 col-md-6 col-sm-6 col-xs-12 tarjeta-producto">
                <img class="imagen-producto" style="width: 150px; height: 100px;" src="images/real.jpg">
                <h1 class="nombre-producto">Camiseta</h1>
                <h3 class="precio-producto">$50.000</h3>
                <div class="descripcion-producto">
                    <p>Camisetas deportivas</p>
                </div>
                <div id="icono" class="div-icono">
                    <i class="las la-cart-arrow-down estilo-icono" onclick="agregarAlCarrito('camiseta', 50000)"></i>
                    <p><b>Agregar al carrito</b></p>
                </div>
            </div>
            
            <div class="tarjeta-total">
                <h2>TOTAL</h2>
                <h2 id="total_carrito">$</h2>
            </div>
        </div>
    </div>
    
</template>
<script>
let carrito = [];
let total = 0;

function agregarAlCarrito(nombre_producto, precio_producto) {
    // alert(nombre + ' ' + precio);
    let producto = { nombre: nombre_producto, precio: precio_producto };
    carrito.push(producto);
    console.log(carrito);
    total = total + precio_producto;
    total_carrito.innerText = '$' + total;
    Swal.fire(
        'Producto agregado',
        'Se ha agregado ' + nombre_producto + ' al carrito de compras',
        'success'
    )
}
</script> -->

