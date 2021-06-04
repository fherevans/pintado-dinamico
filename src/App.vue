<template>
  <div id="app">
    <div class="container" align="center">
      <ul style="list-style-type: none;">

        <li v-for="widget in widgets" :key="widget.id">
          <div class="row mb-3" style="width: 80%; border-style: dotted;">
            <div class="col my-auto" style="text-align: left">
              {{widget.question}}
            </div>
            <div class="col" >

              <div v-if="widget.type==='text'">
                <TextWidget :id="widget.id" :valueSet="widget.valueSet" v-model="widget.answer"></TextWidget>
                {{widget.answer}}
              </div>
              <div v-else-if="widget.type==='checkbox'">
                <div v-for="(widget, index) in widgets" :key="index">
                  <Checkbox @checked="validacionCheckbox" :id="index" :disabled="widget.disabled" :required="widget.required" :max="widget.max" :values="widget.values" :valuesSelected="widget.valuesSelected" :labels="widget.labels"/>
                </div>
              </div>
              <div v-else-if="widget.type==='radius'">
                <h5>Aqu'i el radius></h5>
              </div>
              <div v-else>
                <DropdownWidget :id="widget.id" :label="widget.label" :valueSet="widget.valueSet" :subCategory="widget.subCategory" v-model="widget.selected"></DropdownWidget>
                {{widget.selected}}
              </div>

            </div>
          </div>

        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import TextWidget from './components/TextWidget.vue'
import DropdownWidget from './components/DropdownWidget.vue'
import Checkbox from '@/components/Checkbox';
export default {
  name: 'App',
  components: {
    TextWidget,
    DropdownWidget,
    'Checkbox' : Checkbox
  },
  mounted () {
  },
  data() {
    return{
      widgets : [
          { id : 2,
            question : 'Tu nombre',
            type : 'text',
            valueSet : [16, 2,  true, 'Ana Diana'], //max,min,required, placeholder
            answer : ''
          },
          { id : 3,
            question : 'Tu apellido',
            type : 'text',
            valueSet : [5, 0, false, 'Abc'],
            answer : ''
          },
          { id : 4,
            question : 'Color preferido',
            type : 'dropdown',
            valueSet: [{idSet : 0 , elem : 'Selecciona uno'}, {idSet : 1, elem : 'green'}, {idSet: 2 , elem : 'red'}, {idSet: 3 , elem : 'blue'}, {idSet: 4 , elem : 'yellow'}],
            selected : 0,
            subCategory : []
          },
          { id : 5,
            question : 'Pais preferido',
            type : 'dropdown',
            valueSet: [{idSet : 1, elem : 'USA'}, {idSet: 2 , elem : 'Mexico'}, {idSet: 3 , elem : 'Canada'}],
            selected : 2,
            subCategory: [
                        {idParent : 1,
                          idCat : 1,
                          question : 'Edo favorito',
                          valueSet : [{idSet : 1, name : 'California'}, {idSet: 2, name: 'Las Vegas'} ],
                          selected : 1
                        }
                          ]
          },
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
        }
      ]
    }
  },

  methods: {
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
