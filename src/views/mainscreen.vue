<template>

  <div class="main">
    <div class="headerr mb-2">
      <h3>Guests</h3>

      <button type="button" class="btn  btn-light" @click="clickAdvancedSearchButton">Advanced Search</button>
    </div>

    <div v-if="dataLoaded" class="row">
      <div v-for="(item,index3) in posts.slice(0,arrLimit)" class="col-lg-5ths col-md-2 col-sm-3 mb-2 " :key="index3">
        <input-form v-if="item.type  === 'text'" :selectedItem="item" />
        <select-form v-if="item.type  === 'select'" :selectedItem="item"  />
        <date-form v-if="item.type ==='date'" :selectedItem="item" :dateToChild="dateInfo" :keyofdate="index3" @sendData="updateData"/>
      </div>

    </div>

    <div class="buttons">
      <button type="button" @click="clearButton" class="btn btn-light">Clear</button>
      <button type="button" @click="searchButton" class="btn btn-light">Search</button>
    </div>
      {{posts[9]}}
    <results v-show="searchClicked" :savedFilters="savedFilters" :dateInfo="savedDateInfo" :posts="posts"  />

  </div>


</template>

<script>
import axios from "axios";
import Results from "@/components/results";
import inputForm from "@/components/input-form";
import SelectForm from "@/components/select-form";
import DateForm from "@/components/date-form";

export default {
  name: 'mainscreen',
  components: {DateForm, SelectForm, inputForm, Results,  },
  created() {
    this.getPosts()
  },
  data() {
    return {
      dateInfo: new Date().toISOString().substr(0,10),
      arrLimit:5,
      savedDate2: null,
      savedFilters:[],
      isDate:false,
      searchClicked: false,
      dataLoaded: false,
      posts: [],
      savedDateInfo:'',
      isAdvanced: false,

    }
  },


  methods: {
    async getPosts() {
      const response = await axios
          .get("http://challenge.iperasolutions.com/filters");
      this.posts = response.data
      this.dataLoaded = true;
    },

    clearButton() {
      this.searchClicked = false;
      this.posts.forEach(item => {
        item.value = undefined;
      })
      this.dateInfo=new Date().toISOString().substr(0,10);
    },

    clickAdvancedSearchButton() {
      this.arrLimit = this.arrLimit === 5 ?10 :5
    },

    updateData(dateToChild,key) {
      console.log(key,dateToChild)
      this.posts[key].value = dateToChild
      this.savedDate2 = dateToChild

    },

    searchButton(){
      this.savedFilters=[];
      this.posts.forEach(item=>{
        this.savedFilters.push(item.value);
      })
      this.dateInfo=this.savedDate2
      this.savedDateInfo=this.savedDate2
      this.searchClicked= true;
    },
  },
}


</script>

<style scoped>
.btn {
  border-color: black;
}
.headerr{
  display: flex;
  justify-content: space-between;
}

.buttons {
  margin-top: 3rem;
  display: flex;
  justify-content: flex-end;
}

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