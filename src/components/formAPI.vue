<!--36 Lines of HTML-->
<template>
<div class="form-component">
  <div class="form-container">   

      <div class="form-card-component">
        <h3>Test Api</h3>
        <input type="text" id="email" v-model="email" placeholder="Email">
        <input type="text" id="institutionName"  v-model="cityName" placeholder="City Name">
        <input type="text" id="zipCode"  v-model="zipCode" placeholder="Zip Code">
        <div 
            class="check-credentials-submit"  
            v-bind:class="{ showSubmit: email!=''&& cityName!='' && zipCode!=''}"  
            v-on:click="checkDataValid"
        >CHECK</div>
      </div>

      <div class="form-results">
        <div class="form-results-component">
          <h3>Results</h3>
          <div   v-bind:class="{ green: emailExists }"></div>
          <div   v-bind:class="{ green: cityNameExists }"></div>
          <div   v-bind:class="{ green: zipCodeExists }"></div>
        </div>
      </div>
  </div>

  <div class="message">
      <p>A successful test can be made using any of the data in the json array provided below(email, city, zipcode):</p>
  </div>

  <pre>
     {{userData}}
  </pre>
    
</div>
</template>

<script>
//42 Lines of JS ... a great number
  import axios from 'axios';
  export default {
    name: 'form',
    data () {
      return {
        userData: "",
        email: "",
        cityName: "",
        zipCode: "",
        emailExists: false,
        cityNameExists: false,
        zipCodeExists: false,
        showSubmit: false

      }
    },
    mounted: function(){
      axios.get("http://jsonplaceholder.typicode.com/users")
        .then(response => {
          this.userData = response.data
        })
        .catch(e => {
          this.errors.push(e)
        })
    },
    methods: {
      checkDataValid: function(){
        this.emailExists = false;
        this.cityNameExists = false;
        this.zipCodeExists = false;
        for(var key in this.userData){
           
          if(this.email === this.userData[key].email && this.cityName === this.userData[key].address.city && this.zipCode === this.userData[key].address.zipcode){
            this.emailExists = true;
            this.cityNameExists = true;
            this.zipCodeExists = true;
          }

        }
      }
    }
  }
</script>

<!-- 75 Lines of CSS -->
<style scoped>
  .form-container {
    padding: 10px;
    box-shadow: 0 0 3px black;
    -webkit-border-radius: 18px;
    -moz-border-radius: 18px;
    border-radius: 18px;
    height: 250px;
  }

  .form-container .form-card-component {
    width: 20%;
    display: inline-block;
    float: left;
  }

  .form-container input {
    margin: 5px 0px;
    padding: 5px;
    -webkit-border-radius: 8px;
    -moz-border-radius: 8px;
    border-radius: 8px;
    outline: none;
  }

  .form-container .check-credentials-submit {
    width: 140px;
    height: 30px;
    text-align: center;
    font-size: 1.4rem;
    -webkit-border-radius: 8px;
    -moz-border-radius: 8px;
    border-radius: 8px;
    padding: 7px 10px 0px;
    background-color: #00b8ee;
    cursor: pointer;
    color: #fff;
    outline: none;
    border: none;
    box-shadow: 2px 2px 4px rgba(0, 0, 0, 0.29);
    -webkit-box-shadow: 2px 2px 4px rgba(0, 0, 0, 0.29);
    -moz-box-shadow: 2px 2px 4px rgba(0, 0, 0, 0.29);
    display: none;
  }

  .form-card-component .showSubmit {
    display: block;
  }

  .form-container .check-credentials-submit:hover {
    background-color: #20c9fa;
  }

  .form-container .form-results {
    width: 50%;
    display: inline-block;
    float: left;
  }

  .form-container .form-results-component div {
    width:30px;
    height: 30px;
    margin-top:8px;
    background-color: red;
    display: block;
    border-radius: 20px;
  }

  .form-container .form-results-component .green {
    width:30px;
    height: 30px;
    margin-top:8px;
    background-color: green;
    display: block;
    border-radius: 20px;
  }
</style>