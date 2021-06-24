<template>
  <div >
    <label>{{ selecteditem.title }}</label>
    <select v-model="selecteditem.value"  class="form-select">
      <option
        v-for="(item,index) in selecteditem.options"
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
    selecteditem: {},
  },
}
</script>

<style scoped>

</style>