<template>
  <div>
    <Section :schema="schema" :schemaData="schemaData"></Section>
  </div>
</template>

<script>
 import Section from "../components/Section" 


export default {
  components: {
    Section
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

