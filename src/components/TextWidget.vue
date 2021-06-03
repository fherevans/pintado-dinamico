<template>
  <div class="hello">
    <div class="container my-2">
      <div class="row">
        <input type="text" :value="value"
               :maxlength="valueSet[0]"
               :minlength="valueSet[1]"
               :required="valueSet[2]"
               :placeholder="valueSet[3]"
               @input="$emit('input', $event.target.value)"/>
      </div>
<!--      text class : {{value}}-->
    </div>
  </div>
</template>

<script>
export default {
  props : {
    id: {
      type: Number,
      required: true
    },
    valueSet: {
      type: Array,
      required: true
    },
    answer : {
      type : String
    },
    value : {
      type : String
    }
  },
  name: 'TextWidget',
  
  data(){
    return {
    }
  }
  
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
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
