<template>

  <div class="main">
    <div class="headerr">
      <h3>Guests</h3>

      <button type="button" class="btn btn-light " @click="clickAdvancedSearchButton">Advanced Search</button>
    </div>

    <div v-if="dataloaded" class="grid">
      <div v-for="(selectedItem,index) in posts.slice(0,arrLimit)" :key="index">
        <inputforms v-if="selectedItem.type  === 'text'" :selectedItem="selectedItem"/>
        <selectform v-if="selectedItem.type  === 'select'" :selectedItem="selectedItem" />
        <dateform v-if="selectedItem.type==='date'" :selectedItem="selectedItem" :dateToChild="dateInfo" @sendData="updateData"/>
      </div>

    </div>

    <div class="buttons">
      <button type="button" @click="clearButton()" class="btn btn-light">Clear</button>
      <button type="button" @click="searchclicked= true" class="btn btn-light">Search</button>
    </div>

    <div v-show="searchclicked">

      <ul class="liste">
        <li  v-for="(selectedItem,index) in posts.slice(0,9)" :key="index">
          {{ selectedItem.title }} is : {{ selectedItem.value }}
        </li>
        <li v-for="(selectedItem,index) in posts.slice(9,10)" :key="index">
          {{ selectedItem.title }} is : {{ dateInfo }}
        </li>
      </ul>
    </div>

  </div>


</template>

<script>
import axios from "axios";
import selectform from "@/components/selectform";
import inputforms from "@/components/inputforms";
import Dateform from "@/components/dateform";

export default {
  name: 'mainscreen',
  components: {Dateform, inputforms, selectform},
  created() {
    this.getPosts()
  },
  data() {
    return {

      dateInfo: new Date().toISOString().substr(0,10),
      arrLimit:5,
      isDate:false,
      searchclicked: false,
      dataloaded: false,
      posts: [],
      isAdvanced: false,

    }
  },


  methods: {
    async getPosts() {
      const response = await axios
          .get("http://challenge.iperasolutions.com/filters");
      this.posts = response.data
     // this.posts.forEach(item=>{
     //  item.value=null;
     //  })
      this.dataloaded = true;

    },
    clearButton() {
      this.searchclicked = false;
      this.posts.forEach(item => {
        item.value = null;
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
    }

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