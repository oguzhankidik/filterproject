<template>

  <div class="main">
    <div class="headerr">
      <b>Guests</b>

      <button type="button" class="btn btn-light" v-on:click="isAdvanced= !isAdvanced">Advanced Search</button>
    </div>
      <div class="options">
        <div>

          <label >Location</label>
       <selectform  v-on:childToParent="LocationKey" v-if="dataloaded" v-bind:message="posts[0].options" />

        </div>
        <div>
          <label for="exampleInputName">Name</label>
          <input type="email" class="form-control" id="exampleInputName" placeholder="Name">
          <p>Messages is:</p>
        </div>
        <div>
          <label for="exampleInputEmail">Email</label>
          <input type="email" class="form-control" id="exampleInputEmail" placeholder="Email">
        </div>
        <div>
          <label for="exampleInputPhone">Phone</label>
          <input type="email" class="form-control" id="exampleInputPhone" placeholder="Phone">
        </div>

        <div>
        <label>Nationality</label>
        <selectform v-if="dataloaded" v-on:childToParent="NationalityKey" v-bind:message="posts[4].options"/>
      </div>

      </div>


    <div class="advanced-options" v-show="isAdvanced" >
      <div>
      <label for="checkPassport">Passport Number</label>
      <input type="email" class="form-control" id="checkPassport" placeholder="Name">
    </div>
      <div>
        <label >Gender</label>
        <selectform v-if="dataloaded" v-bind:message="posts[6].options"/>
      </div>

      <div>
        <label for="checkMac">Mac</label>
        <input type="email" class="form-control" id="checkMac" placeholder="Email">
      </div>
      <div>
        <label >Connection Status</label>
        <selectform v-if="dataloaded" v-bind:message="posts[8].options" />
      </div>
      <div>
        <label for="checkDate">Date</label>
        <select class="form-select" aria-label="Default select example" id="checkDate">
          <option selected>(All Times)</option>
          <option value="1">One</option>
          <option value="2">Two</option>
          <option value="3">Three</option>
        </select>
      </div>

    </div>
    <div class="Buttons">
      <button type="button"  class="btn btn-light">Clear</button>
      <button type="button" v-on:click="searchclicked= !searchclicked" class="btn btn-light">Search</button>
    </div>

    <div >
      <div>
        location is : {{locationInfo}}
      </div>
      <div>
        nationality is : {{nationalityInfo}}
      </div>

      </div>
    </div>


</template>

<script>
import axios from "axios";
import selectform from "@/components/selectform";

export default {
  name:'mainscreen',
  components: { selectform},
  created() {
    this.getPosts()
  },
  data() {
    return {
      searchclicked:false,
      dataloaded:false,
      posts: [],
      isAdvanced:false,
      mounted:false,
      locationInfo:'',
      nationalityInfo:'',


    }
  },
    methods: {
      async getPosts() {
        const response=await axios
            .get("http://challenge.iperasolutions.com/filters");
        this.posts=response.data
        this.dataloaded=true;

      },
      LocationKey (value) {
        this.locationInfo = value
      },
      NationalityKey(value) {
        this.nationalityInfo = value
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
.Buttons {

  display: flex;
  justify-content: flex-end;
}
.options{
  display: flex;
  justify-content: center;
}
.form-select{
  width: auto;
}
.advanced-options{
  display: flex;
  justify-content: center;
}
</style>