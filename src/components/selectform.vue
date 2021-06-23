<template>
    <div>
      <b-form-select v-model="selected" v-on:change="emitToParent" :options="options" size="sm" placeholder="sass" class="form-select"></b-form-select>
      <label>{{selected}}</label>
    </div>
</template>

<script>
export default {
  props:{
    message:{

    },

  },
  data() {
    return {

      selected:null,
      options:this.message
    }
  },
  methods: {
    // Define the method that emits data to the parent as the first parameter to `$emit()`.
    // This is referenced in the <template> call in the parent. The second parameter is the payload.
    emitToParent () {
      this.$emit('childToParent', this.selected)
    }
  }
}
</script>

<style scoped>

</style>