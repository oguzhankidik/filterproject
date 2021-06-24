<template>

  <div class="main">
    <div class="headerr">
      <b>Guests</b>

      <button type="button" class="btn btn-light " @click="isAdvanced= !isAdvanced">Advanced Search</button>
    </div>

      <div v-if="dataloaded" class="row">
        <div class="col-md-2" v-for="(selecteditem,index) in posts.slice(0,5)" :key="index">
        <inputforms v-if="selecteditem.type  === 'text'" :selecteditem="selecteditem" />
        <selectform v-if="selecteditem.type  === 'select'" :selecteditem ="selecteditem"  />
        <dateform v-if="selecteditem.type=='date'" :selecteditem="selecteditem" />
        </div>
      </div>


    <div v-if="dataloaded" class="row" v-show="isAdvanced">
      <div class="col-md-2" v-for="(selecteditem,index) in posts.slice(5,10)" :key="index">
        <inputforms v-if="selecteditem.type  == 'text'" :selecteditem="selecteditem"    />
        <selectform v-if="selecteditem.type  == 'select'" :selecteditem ="selecteditem"  />
        <dateform v-if="selecteditem.type =='date'" :selecteditem="selecteditem" />
      </div>

    </div>

    <div class="buttons">
      <button type="button"  @click="clearButton()" class="btn btn-light">Clear</button>
      <button type="button" @click="searchclicked= true" class="btn btn-light">Search</button>
    </div>

    <div v-show="searchclicked">
      <ul class="liste">
        <li  v-for="(selecteditem,index) in posts" :key="index">
          {{selecteditem.title}} is : {{selecteditem.value}}
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
  name:'mainscreen',
  components: {Dateform, inputforms, selectform},
  created() {
    this.getPosts()
  },
  data() {
    return {
      searchclicked:false,
      dataloaded:false,
      posts: [],
      isAdvanced:false,
    }
  },
    methods: {
      async getPosts() {
        const response=await axios
            .get("http://challenge.iperasolutions.com/filters");
        this.posts=response.data
        this.dataloaded=true;

      },
      clearButton(){
        this.searchclicked = false;
        this.posts.forEach( item => {
          item.value = null;
        })
      }
    },
}


</script>

<style scoped>
.btn{
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

.row{
  text-align: center;

  justify-content: center;
}
</style>