<template>
  <div >
    <ul>
      <li  v-for="(selectedItem,index) in savedFilters.slice(0,9)" :key="index">
        {{posts[index].title}} is : {{selectedItem}}
      </li>
      <li v-for="(selectedItem,index2) in posts.slice(9,10)" :key="'A'+index2">
        {{ selectedItem.title }} is : {{dateInfo}}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "results",
  props:{

    posts:{},
    dateInfo:{},
    savedFilters:{},

  },


}
</script>

<style scoped>

</style>