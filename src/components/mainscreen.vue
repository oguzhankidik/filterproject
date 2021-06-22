<template>

  <div class="main">
    <div class="headerr">
      <b>Guests</b>
      <button type="button" class="btn btn-light">Advanced Search</button>
    </div>
      <div class="options">
        <div>
          <label for="select1">Location</label>
          <select class="form-select" aria-label="Default select example" id="select1">
            <option selected>(All Locations)</option>
            <option value="1">One</option>
            <option value="2">Two</option>
            <option value="3">Three</option>
          </select>
        </div>
        <div>
          <label for="exampleInputName">Location</label>
          <input type="email" class="form-control" id="exampleInputName" placeholder="Name">
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
        <label for="select2">Location</label>
        <select class="form-select" aria-label="Default select example" id="select2">
          <option selected>(All Nationalities)</option>
          <option value="1">One</option>
          <option value="2">Two</option>
          <option value="3">Three</option>
        </select>
      </div>

      </div>


    <div class="advanced-options">
      <div>
      <label for="checkPassport">Passport Number</label>
      <input type="email" class="form-control" id="checkPassport" placeholder="Name">
    </div>
      <div>
        <label for="checkGender">Gender</label>
        <select class="form-select" aria-label="Default select example" id="checkGender">
          <option selected>(All Genders)</option>
          <option value="1">One</option>
          <option value="2">Two</option>
          <option value="3">Three</option>
        </select>
      </div>

      <div>
        <label for="checkMac">Mac</label>
        <input type="email" class="form-control" id="checkMac" placeholder="Email">
      </div>
      <div>
        <label for="checkConnection">Connection Status</label>
        <select class="form-select" aria-label="Default select example" id="checkConnection">
          <option selected>(All Connection Statuses)</option>
          <option value="1">One</option>
          <option value="2">Two</option>
          <option value="3">Three</option>
        </select>
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
      <button type="button" class="btn btn-light">Clear</button>
      <button type="button" class="btn btn-light">Search</button>
    </div>

    </div>


</template>

<script>
export default {
  name: "mainscreen"
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