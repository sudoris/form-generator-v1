
<template>
    <div> 
			<fieldset>
				<div v-if="showInputField">
					<label v-bind:for="schema.fieldName">{{ schema.label }}:</label>
					<input id="text-input" type="text" v-bind:name="schema.fieldName" v-model="value[schema.fieldName]">
					{{ value[schema.attrs.dependencies.name] }}|| {{ schema }}
				</div>  
			</fieldset>     
    </div>
</template>

<script>

export default {

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
        
    }
	},
	methods: {
		clearInput() {
			// this.value[this.schema.fieldName] = null
			if ((this.currentFieldName in this.value)) {
				this.$set(this.value, this.currentFieldName, '');
			}
		}
	},
	computed: {
		showInputField() {
			if (this.schema.attrs) {
				if (!(this.schema.attrs.dependencies) || (this.value[this.schema.attrs.dependencies.name] === this.schema.attrs.dependencies.value)) {
					return true
				}else {
				this.clearInput()
					return false
				}	
			}
		}
	}
}
</script>

<style>

</style>