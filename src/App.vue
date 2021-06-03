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
        <div v-for="(widget, index) in widgets" :key="index">
          <Checkbox @checked="validacionCheckbox" :id="index" :disabled="widget.disabled" :required="widget.required" :max="widget.max" :values="widget.values" :valuesSelected="widget.valuesSelected" :labels="widget.labels"/>
        </div>
    </div>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import Checkbox from '@/components/Checkbox';
export default {
  name: 'App',
  components: {
    HelloWorld,
    'Checkbox' : Checkbox,
  },
  mounted () {
      return console.log(this.preguntas); 
  },
  data() {
    return{
      preguntas : [{id : 1, label : 'Tu nombre', tipo : 'texto', valores : {max : 10, min:2, mandatory : true}, respuesta : ''},
                   {id : 2, label: 'Color favorito', tipo : 'selection', valores : ['verde','rojo','rosa'], respuesta : ''}],
      widgets: [
            {
              values: ["primeraCosa","foo2","foo3","foo4"],
              labels : ["primerFoo","foo2","foo3","foo4"],
              valuesSelected: [true,false,false,false],
              id:1,
              min:0,
              required:true,
              max:3,
              disabled: false
            },
            {
              values: ["primeraCosa","foo2","foo3"],
              labels : ["primerFoo","foo2","foo3"],
              valuesSelected: [true,false,false],
              id:1,
              min:0,
              required:true,
              max:3,
              disabled:false
            },
          ],
    }
  },

  methods: {  
    addQuestion(){
      this.preguntas.push({id:this.preguntas.length,tipo:'texto',}) 
    },
    validacionCheckbox: function(value, checked, id) {
      this.widgets[id].valuesSelected[value] = checked;
      let atLeastOne = false;
      let numberSelections = 0;
      this.widgets[id].valuesSelected.forEach((value) => {
        atLeastOne = atLeastOne || value;
        if(value){
            numberSelections += 1;
        }
      });
      if(!atLeastOne && this.widgets[id].required){
          alert("please select one");
      }
      if(numberSelections >= this.widgets[id].max){
          alert("you can not select another one");
          this.widgets[id].disabled = true;
      } else{
          this.widgets[id].disabled = false;
      }
    },
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
