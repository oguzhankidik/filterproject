<template>

  <div class="main">
    <div class="headerr">
      <h3>Guests</h3>

      <button type="button" class="btn btn-light " @click="clickAdvancedSearchButton">Advanced Search</button>
    </div>

    <div v-if="dataloaded" class="grid">
      <div v-for="(selectedItem,index3) in posts.slice(0,arrLimit)" :key="index3">
        <inputforms v-if="selectedItem.type  === 'text'" :selectedItem="selectedItem" />
        <selectform v-if="selectedItem.type  === 'select'" :selectedItem="selectedItem"  />
        <dateform v-if="selectedItem.type==='date'" :selectedItem="selectedItem" :dateToChild="dateInfo"  @sendData="updateData"/>
      </div>

    </div>

    <div class="buttons">
      <button type="button" @click="clearButton()" class="btn btn-light">Clear</button>
      <button type="button" @click="searchButton()" class="btn btn-light">Search</button>
    </div>
    <results v-show="searchclicked" :savedFilters="savedFilters" :dateInfo="savedDateInfo" :posts="posts"  />

  </div>


</template>

<script>
import axios from "axios";
import selectform from "@/components/selectform";
import inputforms from "@/components/inputforms";
import Dateform from "@/components/dateform";
import Results from "@/components/results";

export default {
  name: 'mainscreen',
  components: {Results, Dateform, inputforms, selectform},
  created() {
    this.getPosts()
  },
  data() {
    return {
      dateInfo: new Date().toISOString().substr(0,10),
      arrLimit:5,
      savedFilters:[],
      isDate:false,
      searchclicked: false,
      dataloaded: false,
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

      this.dataloaded = true;

    },
    clearButton() {
      this.searchclicked = false;
      this.posts.forEach(item => {
        item.value = undefined;
      })
      this.dateInfo=new Date().toISOString().substr(0,10);
    },
    clickAdvancedSearchButton(){
      if (this.arrLimit==5){
        this.arrLimit=10
      }
      else this.arrLimit=5
    },
    updateData(dateToChild) {
      this.dateInfo = dateToChild
    },

    searchButton(){
      this.savedFilters.splice(0)
      this.posts.forEach(item=>{
        this.savedFilters.push(item.value);
      })
      this.savedDateInfo=this.dateInfo
      this.searchclicked= true ;
      this.componentKey += 1
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
margin-bottom: 10px;
}

.buttons {
  margin-top: 3rem;
  display: flex;
  justify-content: flex-end;
}

.btn {
  margin-left: 10px;
}

.grid {
  display: grid;
  grid-template-columns: repeat(5 ,1fr);
  grid-column-gap: 10px;
  grid-row-gap: 10px;
  text-align: center;



}
</style>