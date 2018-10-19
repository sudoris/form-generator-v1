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
// Imports

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
			this.$set(this.value, this.schema.fieldName, '');
		}
	},
	computed: {
		showInputField() {
			if (this.schema && this.schema.attrs && this.schema.attrs.dependencies) {
				
				return true
			}
			else {
				this.clearInput()
				return false
			}
		}
	}
// watch: {
//   value: function() {
//     this.$emit('input', this.value)
//   }
// }
}
</script>

<style>

</style>