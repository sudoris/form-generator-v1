<template>      
    <div>
        
          
        <div v-if="showInputField">
            <label v-bind:for="fieldParams.fieldName">{{ fieldParams.label }}:</label>
            <input id="text-input" type="text" v-bind:name="fieldParams.fieldName" v-model="value[fieldParams.fieldName]">
            			
            
        </div>            
    </div>
</template>

<script>
// Imports

export default {
    components: {
        
    },
    props: ['fieldParams', 'value'],
    data () {

        return {
           currentFieldName: this.fieldParams.fieldName
        }
		},
		methods: {
			clearInput() {
				// this.value[this.fieldParams.fieldName] = null
				if ((this.currentFieldName in this.value)) {
					this.$set(this.value, this.currentFieldName, '');
				}
			}
		},
		computed: {
				showInputField() {
					if (this.fieldParams.attrs) {
						if (!(this.fieldParams.attrs.dependencies) || 
							 (this.value[this.fieldParams.attrs.dependencies.name] === this.fieldParams.attrs.dependencies.value)) {
							return true
						}
						else {
							this.clearInput()
							return false
						}
					}

						// if (this.value[this.fieldParams.attrs.dependencies.name] === this.fieldParams.attrs.dependencies.value) {
						// 		return true
						// }
						// else {
						// 		this.clearInput()
						// 		return false
						// }
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