<template>
  <div>
    <label>{{ selectedItem.title }}</label>
    <input type="date" v-model="selectedItem.value" class="form-control">
  </div>
</template>

<script>
export default {
  name: "dateForm",
  props: {
    selectedItem: {
      type :Object,
      default: ()=> {}
    },
  },

  methods: {
  }
}
</script>

<style scoped>

</style>
