<template>
  <div id="app">
    <div class="container" align="center">
      <ul style="list-style-type: none;">
        <li v-for="preg in preguntas" :key="preg.id">
          <div v-if="preg.tipo==='texto'">
            {{preg.label}}
            <HelloWorld datosP = preg.tipo></HelloWorld>
          </div>
          <div v-else>Hola amiwos</div>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'App',
  components: {
    HelloWorld
  },
  mounted () {
      return console.log(this.preguntas); 
  },
  data() {
    return{
      preguntas : [{id : 1, label : 'Tu nombre', tipo : 'texto', valores : {max : 10, min:2, mandatory : true}, respuesta : ''},
                   {id : 2, label: 'Color favorito', tipo : 'selection', valores : ['verde','rojo','rosa'], respuesta : ''}]
    }
  },

  methods: {  
    addQuestion(){
      this.preguntas.push({id:this.preguntas.length,tipo:'texto',}) 
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
