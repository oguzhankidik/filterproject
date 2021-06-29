<template>
  <div >
    <ul>
      <li  v-for="(selectedItem,index) in savedFilters.slice(0,10)" :key="index">
        {{posts[index].title}} is : {{selectedItem}}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "results",
  props:{

    posts:{
    },
    dateInfo:{},
    savedFilters:{
      type :Object,
      default: ()=> []
    },

  },


}
</script>

<style scoped>

</style>