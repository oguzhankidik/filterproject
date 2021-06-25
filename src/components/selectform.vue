<template>
  <div >
    <label >{{ selectedItem.title }}</label>
    <select v-model="selectedItem.value"  class="form-select">
      <option selected disabled :value=null >{{ selectedItem.title }} </option>
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
  name: "selectform",
  props: {
    selectedItem: {},

  },
}
</script>

<style scoped>

</style>