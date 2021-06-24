<template>
<div class="container">
<label>{{selecteditem.title}}</label>
  <input :type="selecteditem.type" v-model="selecteditem.value" class="form-control" :placeholder="selecteditem.title">
</div>
</template>

<script>
export default {
  name: "dateform",
  props:{
    selecteditem:{}
  }
}
</script>

<style scoped>
.container{
  width: 20rem;
}
</style>