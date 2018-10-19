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
        title: "Personal History",
        description: "Personal history of the patient",
        type: "object",
          properties: {
            habits: {
              description: "habits of the patient",
              type: "object",
              fieldName: "habits",
              label: "Habits",
              properties: {
                smoking: {
                  description: "smoking habit",
                  type: "radio",
                  fieldName: "smoking",
                  label: "Smoking",
                  values: ["No", "Yes"]
                }
              }
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

