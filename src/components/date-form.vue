<template>
  <div>
    <label>{{ selectedItem.title }}</label>
    <input :type="date" @change="sendData" v-model="dateToChild" class="form-control">

  </div>
</template>

<script>
export default {
  name: "dateForm",
  props: {
    selectedItem: {},
    dateToChild:{}
  },

  methods: {
    sendData: function () {
      this.$emit('sendData', this.dateToChild);
    },
  }
}
</script>

<style scoped>

</style>