<template>
  <div>
      <div class="container" style="margin-top:20%">
        <div class="row" v-for="(check, index) in values" :key="index">
            <div class="col-sm">
              <input @change="checkByUser(index, $event)" type="checkbox" :name="check" :checked="valuesSelected[index]" :value="values[index]" :disabled="(disabled && !valuesSelected[index])">
              <label>{{ labels[index] }}</label>
            </div>
        </div>
    </div>
  </div>
</template>

<script>

export default {
    name: "Checkbox",
      props: {
        id: {
          type: Number,
          required: true
        },
        required: {
          type: Boolean,
          required: true
        },
        disabled: {
          type: Boolean,
          required: true
        },
        max: {
          type: Number,
          required: true
        },
        values: {
          type: Array,
          required: true
        },
        valuesSelected: {
          type: Array,
          required: true
        },
        labels: {
          type: Array,
          required: true
        },
      },
    data: function () {
        return {
        }
    },
    methods: {
      checkByUser: function(index, event) {
          this.$emit('checked', index, event.target.checked, this.$props.id);
      },
    },
}
</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
h3 {
  margin: 40px 0 0;
  display: block;
  margin-top: 2.7em;
  font-weight: bold;
  color: rgb(7, 7, 7);
}
</style>