<template>
    <div>     
        <fieldset>     
					<div v-for="(item, index) in schema.values" :key="index">
						<input type="checkbox" :id="item" :value="item" v-model="value[schema.fieldName]">
          	<label :for="item">{{ item }}</label>
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
        return  {}
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
      this.$set(this.value, this.currentFieldName, []);
      //this.value["keyOnCreate"] = {};
      this.$emit("input", this.value);
    }
  }
}
</script>

<style>

</style>