<template>
  <div>    
    <div v-for="(field, key) in schema.properties" :key="key">   
      <component 
        :is="getComponentName(field.type)" 
        v-bind:schema="field"
        v-model="value[currentFieldName]">         
      </component>
    </div>
  </div>
</template>

<script>
import TextInput from "../input_components/TextInput"
import RadioInput from "../input_components/RadioInput"
import CheckList from "../input_components/CheckList"

export default {
  name: 'ObjectComponent',
  components: {
    TextInput,
    RadioInput,
    CheckList
  },
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
        return {}
      }
    }
  },
  data () {
      return {
          currentFieldName: this.schema.fieldName
      }
  },
  created: function() {
      if (!(this.currentFieldName in this.value)) {
        // this.value[this.currentFieldName] = {}
        // this.$emit('input', this.value)
        this.$set(this.value, this.currentFieldName, {});
        //this.value["keyOnCreate"] = {};
        this.$emit("input", this.value);
      }
  },
  methods: {        
    getComponentName(type) {
      switch (type) {
        case "text":
          return "TextInput"
          
        case "radio":
          return "RadioInput"

        case "checklist":
          return "CheckList"

        case "object": 
          return "ObjectComponent"
      }
    }      
  },
    
}
</script>

<style>

</style>