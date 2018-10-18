<template>
  <div>
    <div v-for="(field, key) in sectionSchema.properties" :key="key">   
        
      <fieldset>
        <!-- <div class="field-title"></div> -->
        <legend class="field-title">{{ field.description}}</legend>          
        <component :is="getComponentName(field.type)" v-bind:fieldParams="field" v-model="sectionData" ></component>
        
      </fieldset>
      
      <br>
    </div>

    
    {{ sectionData }}
  </div>
</template>

<script>
import TextInput from "./input_components/TextInput"
import RadioInput from "./input_components/RadioInput"
import CheckList from "./input_components/CheckList"
import ObjectComponent from "./utility_components/ObjectComponent"

export default {
  name: 'Section',
  components: {
    TextInput,
    RadioInput,
    ObjectComponent,    
    CheckList
  },
  methods: {        
    getComponentName(type) {
      if (type === 'string') {
        return 'TextInput'
      }
      else if (type === 'radio') {
        return 'RadioInput'
      }
      else if (type === 'object') {
        return 'ObjectComponent'
      }
      else if (type === 'checklist') {
        return 'CheckList'
      }
    },
    initEmptyObject(objectKey) {
      this.sectionData[objectKey] = {}
    }
    
    // currentProps(field) {
    //   return field
    // }
  },
  computed: {
    
  },
  data() {
    return {      
      sectionData: { 
          allergies: {
            hasAllergies: "Yes"
          }
      },
      sectionSchema: {
        $schema: "http://json-schema.org/draft-07/schema#",
        $id: "http://example.com/product.schema.json",
        title: "Test",
        description: "Dependencies Test",
        type: "object",
        properties: {
          allergies: {
            description: "Drug Allergies",
            type: "object",
            fieldName: "allergies",
            label: "Drug Allergies",            
            properties: {
              hasAllergies: {
                description: "allergies",
                type: "radio",
                fieldName: "hasAllergies",
                label: "Does patient have any known drug allergies?",
                values: ['Yes', 'No'],                
              },
              allergiesList: {
                description: "List all drug allergies",
                type: "string",
                fieldName: "allergiesList",
                label: "Enter drug allergies",
                attrs: {
                  hidden: true,
                  dependencies: {
                    name: 'hasAllergies',
                    value: 'Yes'
                  }
                }
              },
              severity: {
                description: 'severity level',
                type: 'object',
                fieldName: 'severity',
                label: 'Severity Level',
                attrs: {
                  dependencies: {
                    name: 'allergiesList',
                    value: 'ok'
                  }
                },
                properties: {
                  lifeThreatening: {
                    description: "Life threatening",
                    type: 'radio',
                    fieldName: 'lifeThreatening',
                    label: 'Is drug life threatening',
                    values: ['Yes', 'No']
                  },
                  someText: {
                    description: "someText",
                    type: "string",
                    fieldName: "someText",
                    label: "someText",
                    attrs: {
                      hidden: true,
                      dependencies: {
                        name: 'lifeThreatening',
                        value: 'Yes'
                      }
                    }
                  }

                }
              }
            }
          }     
          // allergies: {
          //   description: "drug allergies field",
          //   type: "radio",
          //   fieldName: "allergies",
          //   label: "Drug Allergies",
          //   values: ['Yes', 'No']
          // }     
        }         
      }
      // end sectionSchema
        
    }
    // end return
  }
  // end data
}
</script>

<style>
.field-title {
  color: blueviolet;
}

</style>
