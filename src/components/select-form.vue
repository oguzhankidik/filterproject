<template>
  <div >
    <label >{{ selectedItem.title }}</label>
    <select v-model="selectedItem.value"  class="form-select">
      <option selected disabled :value=null >(All {{ selectedItem.title }}) </option>
      <option
        v-for="(item,index) in selectedItem.options"
        :key="index"
        :value="item.value">
        {{ item.text }}
      </option>
    </select>

  </div>
</template>

<script>
export default {
  name: "selectForm",
  props: {
    selectedItem: {
      type :Object,
      default: ()=> {}
    },

  },

}
</script>

<style scoped>

</style>
