<template>
  <div class="form-row form-group">
    <div class="col my-2">
      <select style="width: 90%;"
              :value="value"
              @input="$emit('input', $event.target.value)">
        <option :value="elem.idSet" v-for="elem in valueSet" :key="elem.idSet">{{elem.elem}}</option>
      </select>
<!--      <div v-if="subCategory.length !== 0">-->
<!--        <div v-for="element in subCategory" :key="element.idCat">-->
<!--          <div v-if="value===element.idParent">-->

<!--          </div>-->
<!--        </div>-->
<!--      </div>-->
    </div>
  </div>
</template>

<script>
export default {
  props: {
    id: {
      type: Number,
      required: true
    },
    valueSet: {
      type: Array,
      required: true
    },
    selected: {
      type: String
    },
    value: {
      type: Number
    },
    subCategory : {
      type : Array
    },
    label : {
      type: String
    }
  },

}
</script>