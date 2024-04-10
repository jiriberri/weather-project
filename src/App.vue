<template>
  <div id="app" :class="typeof weather.main != 'undefined' && weather.main.temp > 17 ? 'warm' : ''">
    <main>
      <div class="search-section">
        <input 
          type="text"
          class="search-bar"
          placeholder="Search"
          v-model="query"
          @keyup.enter="fetchWeather"
        >
      </div>

      <div class="weather-location" v-if="typeof weather.main != 'undefined'">
        <div class="location-section">
          <div class="location">{{ weather.name }}, {{ weather.sys.country }}</div>
          <div class="date">{{ dateBuilder() }}</div>
        </div>
      </div>

      <div class="weather-section" v-if=" typeof weather.main != 'undefined'">
        <div class="temperature">{{ Math.round(weather.main.temp) }}°C</div>
        <div class="weather">{{ weather.weather[0].main }}</div>

      </div>
    </main>
  </div>
</template>

<script>

export default {
  name: 'App',
  data () {
    return {
      api_key: '642f37328cb1fc0a2c281c1289fe2e51',
      url_base: 'http://api.openweathermap.org/data/2.5/',
      query: '',
      weather: {}
    } 
  },

  methods: {
    fetchWeather() {
      fetch(`${this.url_base}weather?q=${this.query}&units=metric&APPID=${this.api_key}`)
      .then(response => {
        return response.json();
      }).then(this.setResults);
    },

    setResults(data) {
      this.weather = data;
      console.log(this.weather);
    },

    dateBuilder () {
      let d = new Date();
      let months = ["January", "February", "March", "April", "May",
      "June", "July", "August", "September", "October", "November", "December"];
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
  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    transition: 0.4s;
  }

  body {
    font-family: 'roboto', sans-serif;
  }

  #app {
    background-image: url(./assets/cold.jpg);
    background-size: cover;
    background-position: bottom;
  }

  #app.warm {
    background-image: url(./assets/warm.jpg);
  }

  main {
    min-height: 100vh;
    padding: 25px;

    background-image: linear-gradient(to bottom, rgba(0,0,0, 0.1), rgba(0,0,0, 0.50));
  }

  .search-section {
    widows: 100%;
    margin-bottom: 30px;

  }

  .search-section .search-bar {
    display: block;
    width: 100%;
    padding: 15px;

    color: #1f1f1f;
    font-size: 22px;

    appearance: none;
    border: none;
    outline: none;

    background-color: rgba(255, 255, 255, 0.6);
    border-radius: 3px 20px 3px 20px;
    box-shadow: 12px 15px 10px rgba(0, 0, 0, 0.1);
  
  }

  .search-section .search-bar:focus {
    box-shadow: 12px 15px 10px rgba(0, 0, 0, 0.25);
    background-color: rgba(255, 255, 255, 0.8);
    border-radius: 20px 3px 20px 3px;
  }

  .location-section .location{
    color: #fff;
    font-size: 32px;
    font-weight: 500;
    text-align: center;
    text-shadow: 1px 3px rgba(0, 0, 0, 0.25);
  }

  .location-section .date{
    color: #fff;
    font-size: 20px;
    font-weight: 300;
    font-style: italic;
    text-align: center;
  }

  .weather-section {
    text-align: center;
  }

  .weather-section .temperature {
    display: inline-block;
    padding: 10px 25px;
    color: #fff;
    font-size: 102px;
    font-weight: 900;
    text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
    background-color: rgba(255, 255, 255, 0.25);
    border-radius: 20px;
    margin: 30px 0px;
    box-shadow: 12px 15px 10px rgba(0, 0, 0, 0.2);
  }

  .weather-section .weather {
    display: block;
    color: #fff;
    text-shadow: 4px 5px rgba(0, 0, 0, 0.25);
    font-size: 50px;
    font-weight: 700;
    font-style: italic;
    
  }

</style>
