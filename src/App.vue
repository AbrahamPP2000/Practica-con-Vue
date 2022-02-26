<template>
  <div id="app">
    <img src="./assets/logo.png">
    <h1 v-bind:class = "titleClass">Practicando lo aprendido en vuejs.org con un Vue.js App</h1>
    <p>La cuenta es: {{contadores.cont}}</p>
    <button v-on:click="prueba">prueba: {{contadores.cont}}</button>
    <h2>Eventos DOM con botones de incremento y decremento</h2>
    <button v-on:click="incremento1">Incremento de 1 en 1: {{cuentaDe1en1}}</button>
    <button v-on:click="incremento2">Incremento de 2 en 2: {{cuentaDe2en2}}</button>
    <button @click="decremento1">Decremento de 1 en 1: {{cuentaRegresivaDe1en1}}</button>
    <button @click="decremento2">Decremento de 2 en 2: {{cuentaRegresivaDe2en2}}</button>
    <h2>Prueba de despliegue de texto de un buscador con v-model</h2>
    <input v-model="texto" placeholder="Escriba aquí">
    <p>{{texto}}</p>
    <h2>Prueba de condicionales v-if y v-else</h2>
    <input v-model="edad" placeholder="Ingrese su edad">
    <button @click="esMayorDeEdad">Verificar</button>
    <p v-if="mayorDeEdad">Es mayor de edad</p>
    <p v-else>Es menor de edad</p>
    <p v-if="edadImposible">{{mensajeAdverteneciaEdad}}</p>
    <h2>Despliegue de los elementos de un arreglo con v-for y tacharlos</h2>
    <input v-model="nuevoTanque" @keyup.enter="agregarTanque">
    <button @click="agregarTanque">Agregar tanque</button>
    <ul>
    <li v-for="tanque in tanquesFiltrados" :key="tanque.id">
      <input type="checkbox" v-model="tanque.done" />
      <span :class="{ done: tanque.done }">{{ tanque.text }}</span>
      <button @click="eliminarTanque(tanque)">X</button>
    </li>
    <button @click="ocultamientoCompletado = !ocultamientoCompletado">
    {{ ocultamientoCompletado ? 'Mostrar todos' : 'Ocultamiento completado' }}
    </button>
    </ul>
    <h2>Prueba de referencia a una plantilla</h2>
    <p ref="contenido">Texto</p>
    <h2>Monitoreo de un contador</h2>
    <p>{{contadorParaObservacion}}</p>
    <!--
    <h2>Essential Links</h2>
    <ul>
      <li><a href="https://vuejs.org" target="_blank">Core Docs</a></li>
      <li><a href="https://forum.vuejs.org" target="_blank">Forum</a></li>
      <li><a href="https://chat.vuejs.org" target="_blank">Community Chat</a></li>
      <li><a href="https://twitter.com/vuejs" target="_blank">Twitter</a></li>
    </ul>
    <h2>Ecosystem</h2>
    <ul>
      <li><a href="http://router.vuejs.org/" target="_blank">vue-router</a></li>
      <li><a href="http://vuex.vuejs.org/" target="_blank">vuex</a></li>
      <li><a href="http://vue-loader.vuejs.org/" target="_blank">vue-loader</a></li>
      <li><a href="https://github.com/vuejs/awesome-vue" target="_blank">awesome-vue</a></li>
    </ul>
    -->
  </div>
</template>

<script>
let idListaTanques = 0
export default {
  mounted() {
    this.$refs.contenido.textContent = 'Contenido de la referencia'
  },
  name: 'app',
  data () {
    return {
      titleClass: 'claseTitulo',
      //msg: 'Practicando lo aprendido en vuejs.org con un Vue.js App',
      contadores: {
        cont: 0,
      },

      cuentaDe1en1: 0,
      cuentaDe2en2: 0,
      cuentaRegresivaDe1en1: 0,
      cuentaRegresivaDe2en2: 0,

      texto: '',

      edad: '',
      mayorDeEdad: true,
      edadImposible: false,
      mensajeAdverteneciaEdad: 'Esa edad es imposible',

      nuevoTanque: '',
      listaTanques: [
        {id: idListaTanques++, text: 'T-34/85', done: true},
        {id: idListaTanques++, text: 'Tiger I', done: false}
      ],

      ocultamientoCompletado: false,

      contadorParaObservacion: 0
    }
  },
  computed: {
    tanquesFiltrados() {
      return this.ocultamientoCompletado
        ? this.listaTanques.filter((t) => !t.done)
        : this.listaTanques
    }
  },
  methods: {
    incremento1() {
      this.cuentaDe1en1++
    },
    incremento2() {
      this.cuentaDe2en2+=2
    },
    decremento1() {
      this.cuentaRegresivaDe1en1--
    },
    decremento2() {
      this.cuentaRegresivaDe2en2-=2
    },
    prueba(){
      this.contadores.cont++
    },
    esMayorDeEdad(){
      if(Number(this.edad) < 18 && Number(this.edad) >= 0){
        this.mayorDeEdad = false
      }else if(Number(this.edad) >= 18 && Number(this.edad) <= 130){
        this.mayorDeEdad = true
      }else{
        this.edadImposible = true
      }
    },
    agregarTanque() {
      this.listaTanques.push({ id: idListaTanques++, text: this.nuevoTanque, done: false })
      this.nuevoTanque = ''
    },
    eliminarTanque(tanque) {
      this.listaTanques = this.listaTanques.filter((t) => t !== tanque)
    }
  },
  watch: {
    contadorParaObservacion(nuevoContador) {
      console.log(`La nueva cuenta es: ${nuevoContador}`)
    }
  }
}


</script>

<style>
.claseTitulo{
  color: blue;
}

.done {
  text-decoration: line-through;
}

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h1, h2 {
  font-size: 150%; 
}

h2 {
  color: green;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
