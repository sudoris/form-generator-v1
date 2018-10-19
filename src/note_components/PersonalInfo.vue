<template>
  <div>
    <VueSchema :schema="schema" :schemaData="schemaData"></VueSchema>
  </div>
</template>

<script>
 import VueSchema from "../components/VueSchema" 


export default {
  components: {
    VueSchema
  },
  data() {
    return {
      schemaData: {},
      schema: {
        $schema: "http://json-schema.org/draft-07/schema#",
        $id: "http://example.com/product.schema.json",
        title: "Personal Information",
        description: "Information of the patient",
        type: "object",
        properties: {
          name: {
            description: "",// legend data
            type: "text",//type of input
            fieldName: "name",//schemaData key
            label: "Name",// label data
          }
        },
        required: [ "productId" ]
      }
    }
  },

}
</script>

<style>

</style>

