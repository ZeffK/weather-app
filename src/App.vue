<template>
  <div id="app">

    <div id='main'>

    <div class="search-box"> 
      <input type="text" name="" id="" class="search-bar" placeholder="Search..." v-model="query"
       @keypress="fetchWeather"
       >
    </div>
<div v-if="fetched">
  <h1>You are searching for: {{query}}  </h1>
  <p> Name: {{weather.name}} <br> climate: {{fetchdis}} </p>
</div>
<div class="weather-wrap" v-if=" typeof weather.main !='undefined'">
      <div class="location-box">

      <div class="location"> {{weather.name}}, {{weather.sys.country}} </div>
      <div class="date"> Monday 12 May 2020</div>
          </div>

      <div class="weather-box">
  
        <div class="temp">40 </div>
        <div class="weather"> Hot</div>
        
        </div>
</div>

    
  </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'app',
  data(){
    return{
      api_key:'3c63c33183a4e2b226d10d7d6fe103d9',
      url_base:'https://api.openweathermap.org/data/2.5/',
      query:'',
      weather:{},
      fetched:false
      
    }
  },
  methods:{
   fetchWeather (e) {
      if (e.key == "Enter")
      
      {
           axios.get('https://api.openweathermap.org/data/2.5/weather',{ 
              params:{
                 q: this.query,
                  appid: this.api_key
                 
              }
          }).then(response=>{
              this.weather = response.data;
              console.log(this.weather.name);
          }).then(this.fetched=true);
          
          
      }
    },

   

    
  },


  computed:{

   fetchdis(){
      var j = this.weather.weather[0];
      console.log(j);
       return j.description;
    }
  }
  
    
  }


  
</script>


<style>

 

.weather-box  {
  text-align: center;
}

.location-box{
  text-align: center;
}

.search-box{
  text-align: center;
}

</style>
