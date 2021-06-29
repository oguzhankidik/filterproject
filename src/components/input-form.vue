<template>
  <div >
  <label>{{selectedItem.title}}</label>
  <input :type="selectedItem.type" v-model="selectedItem.value" class="form-control" :placeholder=selectedItem.title>

  </div>
</template>

<script>
export default {
  name: "inputForm",
  props:{
    selectedItem: {}
  },
  methods:{

  }
}
</script>

<style scoped>


</style>