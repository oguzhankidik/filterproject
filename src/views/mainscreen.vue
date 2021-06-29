<template>

  <div class="main">
    <div class="d-flex justify-content-between mb-2">
      <h3>Guests</h3>
      <button type="button" class="btn  btn-outline-secondary" @click="clickAdvancedSearchButton">Advanced Search</button>
    </div>

    <div v-if="dataLoaded" class="row">
      <div v-for="(item,index3) in posts.slice(0,arrLimit)" class="col-lg-2 col-md-6 col-sm-6 col-12 mb-2 " :key="index3">
        <input-form v-if="item.type  === 'text'" :selectedItem="item" />
        <select-form v-if="item.type  === 'select'" :selectedItem="item"  />
        <date-form v-if="item.type ==='date'" :selectedItem="item"/>
      </div>

    </div>

    <div class="d-flex justify-content-end mt-5">
      <button type="button" @click="clearButton" class="btn btn-outline-secondary">Clear</button>
      <button type="button" @click="searchButton" class="btn btn-outline-secondary">Search</button>
    </div>

    <div v-if="searchClicked" >
      <ul>
        <li  v-for="(item,index) in savedFilters" :key="index">
          {{item.title}} is : {{item.value}}
        </li>
      </ul>
    </div>
  </div>


</template>

<script>
import axios from "axios";

import inputForm from "@/components/input-form";
import SelectForm from "@/components/select-form";
import DateForm from "@/components/date-form";

export default {
  name: 'mainscreen',

  components: {DateForm, SelectForm, inputForm  },

  created() {
    this.getPosts()
  },

  data() {
    return {

      arrLimit:5,
      savedFilters:[],
      isDate:false,
      searchClicked: false,
      dataLoaded: false,
      posts: [],
      isAdvanced: false,

    }
  },


  methods: {
    async getPosts() {
      let response = await axios.get("http://challenge.iperasolutions.com/filters");

      response.data.forEach( item => {
        if(item.type === 'select'){
          item.value = null
        } else if( item.type === 'text') {
          item.value = ''
        } else {
          item.value = new Date().toISOString().slice(0,10)
        }
        this.posts.push(item)
      })
      this.dataLoaded = true;
    },

    clearButton() {
      this.searchClicked = false;
      this.posts.forEach(item => {
        if(item.type === 'select'){
          item.value = null
        } else if( item.type === 'text') {
          item.value = ''
        } else {
          item.value = new Date().toISOString().slice(0,10)
        }
      })
      this.dateInfo = new Date().toISOString().substr(0,10);
    },

    clickAdvancedSearchButton() {
      this.arrLimit = this.arrLimit === 5 ? 10 :5
    },

    searchButton(){

      this.savedFilters = JSON.parse(JSON.stringify(this.posts))
      this.searchClicked= true;
    },
  },
}


</script>

<style scoped>


.btn {
  margin-left: 10px;
}

.col-lg-5ths {
  position: relative;
  min-height: 1px;
  padding-right: 15px;
  padding-left: 15px;
}

</style>
