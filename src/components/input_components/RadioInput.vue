<template>
  <div>
    <fieldset>
      <legend>{{ schema.label }}</legend>      
      <span v-for="(item, index) in schema.values" :key="index">
        <input type="radio" :id="item" :value="item" v-model="value[schema.fieldName]">
        <label :for="item">{{ item }}</label>
      </span>
    </fieldset>
  </div>
</template>

<script>


export default {
  //value = schemaData. v-model default prop is value
  props: {
    schema: {
      type: Object,
      default() {
        return {}
      }
    },
    value: {
      type: Object,
      default() {
        return  {}
      }
    }
  },
  data () {
    return {

    }
  }
}
</script>

<style>
 
</style>