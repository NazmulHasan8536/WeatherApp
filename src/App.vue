<template>
  <div id="app" :class="typeof weather.main !='undefined' && weather.main.temp > 16 ? 'warm': ''">
    <main>
      <div class="title">
        <h2>{{title}}</h2>
        <!-- <p>Search Country name or Capital or District name</p> -->
      </div>

      <div class="search-box"> 
        <input type="text" id="search" class="search-bar" placeholder="Search....." v-model="query" @keypress="fetchWeather">
      </div>

      <div class="wheater-wrap" v-if="typeof weather.main != 'undefined'">
        <div class="location-box">
          <div class="location">{{weather.name}} , {{weather.sys.country}}</div>
          <div class="date">{{dateBuilder()}}</div>
        </div>


        <div class="wheater-box">
          <div class="temp">{{ Math.round(weather.main.temp) }}°  c</div>
          <div class="weather">{{weather.weather[0].main}}</div>
        </div>

      </div>

    </main>
    </div>
</template>

<script>

export default {
  name: 'App',
  data(){
    return{
      title:'Weather App',
      api_key:'b2376d7e6460c294a9af7d3b62a6f41f',
      url_base:'https://api.openweathermap.org/data/2.5/',
      query:'',
      weather: {}
    }
  },
  methods:{
    fetchWeather(e){
      if(e.key == 'Enter'){
        fetch(`${this.url_base}weather?q=${this.query}&units=metric&APPID=${this.api_key}`)
        .then(res =>{
          return res.json();
        }).then(this.setResults);
      }
    },
    setResults(results){
      this.weather = results;
    },

      dateBuilder () {
      let d = new Date();
      let months = ["January", "February", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December"];
      let days = ["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"];
      let day = days[d.getDay()];
      let date = d.getDate();
      let month = months[d.getMonth()];
      let year = d.getFullYear();
      return `${day} ${date} ${month} ${year}`;
    }

  }
 
}
</script>

<style>
  *{
    margin:0;
    padding:0;
    box-sizing: border-box;
  }
  body{
    font-family: 'montserrat',sans-serif;
  }
  #app{
    background-image: url('./assets/Rainy.jpg');
    background-size: cover;
    background-position: bottom;
    transition: 0.4s;
  }
  #app.warm{
    background-image: url('./assets/sunny.jpg');
  }
  main{
    min-height:100vh;
    padding:25px;

    background-image: linear-gradient(bottom,rgba(0,0,0,.25),rgba(0,0,0,.75));    
  }
  .title{
    margin:10px 0;
  }
  .title h2{
    text-align: center;
    color:#fff;
    font-size: 32px;
    font-weight: 500;
    text-align: center;
    text-shadow: 1px 3px rgba(0,0,0,.75);
  }
  .title p{
    text-align: center;
    color:#fff;
    font-size: 18px;
    font-weight: 500;
    text-align: center;
    text-shadow: 1px 3px rgba(0,0,0,.75);
    padding:10px 0;
  }
  .search-box{
    width:100%;
    margin-bottom: 10px;
  }
  .search-box .search-bar{
    display: block;
    width:100%;
    padding:15px;

    color:#313131;
    font-size: 20px;

    appearance: none;
    border:none;
    outline: none;
    background: none;

    box-shadow: 0px 0px 8px rgba(0,0,0,.25);
    background-color: rgba(255,255,255,.5);
    border-radius: 0px 16px 0px 16px;
    transition: 0.4s;
  }
  .search-box .search-bar:focus{
    box-shadow: 0px 0px 16px rgba(0,0,0,.25);
    background-color: rgba(255,255,255,.75);
    border-radius: 16px 0px 16px 0px;
  }
  .location-box .location{
    color:#fff;
    font-size: 32px;
    font-weight: 500;
    text-align: center;
    text-shadow: 1px 3px rgba(0,0,0,.25);

  }
  .location-box .date{
     color:#fff;
    font-size: 32px;
    font-weight: 300;
    text-align: center;
    font-style: italic;
  }
  .wheater-box{
    text-align: center;
  }
  .wheater-box .temp{
    display:inline-block;
    padding: 10px 25px;
    color:#fff;
    font-size: 102px;
    font-weight: 900;

    text-shadow: 3px 6px rgba(0,0,0,.25);
    background-color: rgba(255,255,255,.25);
    border-radius: 16px;
    margin:30px 0;

    box-shadow: 3px 6px rgba(0,0,0,.25);
    
  }
  .wheater-box .weather{
    color:#fff;
    font-size: 48px;
    font-weight: 700;
    font-style: italic;
    text-shadow: 3px 6px rgba(255,255,255,.25) ;
  }
  

</style>
