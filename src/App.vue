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
                <h5>Aqui va checkbox</h5>
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

export default {
  name: 'App',
  components: {
    TextWidget,
    DropdownWidget
  },
  mounted () {
    return console.log(this.widgets);
  },
  data() {
    return{
      widgets : [
          { id : 2,
            question : 'Tu nombre',
            type : 'text',
            valueSet : [10, 2,  true, 'Ana Diana'], //max,min,required, placeholder
            answer : ''
          },
          { id : 3,
            question : 'Tu apellido',
            type : 'text',
            valueSet : [5, 0, false, 'Ana Diana'],
            answer : ''
          },
          { id : 4,
            question : 'Color preferido',
            type : 'dropdown',
            valueSet: [{idSet : 1, elem : 'green'}, {idSet: 2 , elem : 'red'}, {idSet: 3 , elem : 'blue'}],
            selected : 2,
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
          }
      ]
    }
  },
  methods: {  

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
