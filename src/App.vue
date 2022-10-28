<style>
  @import 'main.css';
</style>

<template>
  <div id="app" :class="typeof weather.main != 'undefined' && weather.main.temp > 16 ? 'warm' : ''">
    <main>
      <div class="search-box">
        <input 
        type="text" 
        class="search-bar" 
        placeholder="Where are you?" 
        v-model="query"
        @keypress.enter="fetchWeather">
        <div class="info" style="min-height:25px;">
          <p v-if="query">Press Enter to search!</p>
        </div>
      </div>

      <!-- weather -->
      <div class="weather-wrap" v-if="typeof weather.main != 'undefined'">
        <div class="location-box">
          <div class="location">{{weather.name}}, {{weather.sys.country}}</div>
          <div class="date">{{ todaysDate() }}</div>
        </div>
        <div class="weather-box">
          <div class="temp">
            {{ Math.round(weather.main.temp) }}°c
          </div>
          <div class="weather-status">
            {{ weather.weather[0].main}}
          </div>
        </div>
      </div>
    </main>
    
  </div>
</template>

<script>

export default {
  name: 'App',
  data (){
    return {
      api_key : 'a1b350e794de3e9cf027a0d7ab4d19fc',
      url_base : 'http://api.openweathermap.org/geo/1.0/direct',
      one_call_url : 'https://api.openweathermap.org/data/2.5/weather',
      query: '',
      weather : {},
      geoLocation : {
        lat : null,
        lon : null,
      },
      icon: 0,
    }
  }, methods : {
    fetchWeather() {
      fetch(`${this.url_base}?q=${this.query}&limit=1&appid=${this.api_key}`)
      .then(res => {
        return res.json();
      }).then(this.setGeoLocation);
    },
    setGeoLocation(results){
      this.geoLocation.lat = results[0].lat;
      this.geoLocation.lon = results[0].lon;
      fetch(`${this.one_call_url}?lat=${this.geoLocation.lat}&lon=${this.geoLocation.lon}&units=metric&appid=${this.api_key}`)
      .then(res => {
        return res.json();
      }).then(this.setResults);
    }
    ,
    setResults(results){
      this.weather = results;
    },
    todaysDate(){
      let d = new Date();
      let months = ["January", "February", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December"];
      let days = ["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"];
      let day = days[d.getDay()];
      let date = d.getDate();
      let month = months[d.getMonth()];
      let year = d.getFullYear();
      return `${day}, ${date} ${month}, ${year}`;
    }
  }
}
</script>

<style>
  
</style>
