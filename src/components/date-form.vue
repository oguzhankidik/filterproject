<template>
  <div>
    <label>{{ selectedItem.title }}</label>
    <input type="date" @change="sendData" v-model="dateToChild" class="form-control">
<label>{{keyofdate}}</label>
  </div>
</template>

<script>
export default {
  name: "dateForm",
  props: {
    selectedItem: {
      type :Object,
      default: ()=> []
    },
    keyofdate:{
      required :true
    },
    dateToChild:{},

  },

  methods: {
    sendData: function (event) {
      this.$emit('sendData', event.target.value,this.keyofdate);
    },
  }
}
</script>

<style scoped>

</style>