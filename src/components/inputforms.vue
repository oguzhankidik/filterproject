<template>
  <div >
  <label>{{selecteditem.title}}</label>
  <input :type="selecteditem.type" v-model="selecteditem.value" class="form-control" :placeholder=selecteditem.title>

  </div>
</template>

<script>
export default {
  name: "inputforms",
  props:{
    selecteditem: {}
  }
}
</script>

<style scoped>


</style>