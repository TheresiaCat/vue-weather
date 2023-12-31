<template>
  <div id="app" :class="getBackgroundClass()">
    <main>
      <!--Searchbox-->
      <!--@ is short version of v-on-->
      <div class="search-box">
        <input 
          type="text" 
          class="search-bar" 
          placeholder="Search for a Place..."
          v-model="query"
          @keypress="fetchWeather"
        />
      </div>

      <!--General Information-->
      <!--Important to use the same variables as the API response see https://openweathermap.org/current-->
      <div class="weather-wrap" v-if="typeof weather.main != 'undefined'">
        <div class="location-box">
          <div class="location">{{ weather.name }}, {{ weather.sys.country }}</div>
          <div class="date">{{ getCurrentDate() }}</div>
        </div>  
      </div>

      <!--Weather Information-->
      <div class="weather-box" v-if="typeof weather.main != 'undefined'">
          <div class="temp">{{weather.main.temp.toFixed(0)}}°c</div>
          <div class="weather">{{ weather.weather[0].description }}</div>
      </div>

      <!-- Intro Message -->
      <div class="intro-message" v-if="typeof weather.main === 'undefined' && query.length > 0">
        Type an existing city name and press enter.
      </div>
    </main>
  </div>
</template>

<script>
export default {
  name: 'App', 
  
  //Get Object back
  data () {
    return {
      api_key: '4a9c3f1322b526b57e2c80a1e33c49e4',
      url_base: 'https://api.openweathermap.org/data/2.5/',
      query: '',
      weather: {} //default empty object
    }
  },

  
  methods: {
    // Method to get todays weather Data
    //e is event 
    //start by hitting Enter 
    //get response in json
    fetchWeather (e) {
      if (e.key == "Enter")
      fetch(`${this.url_base}weather?q=${this.query}&units=metric&APPID=${this.api_key}`)
          .then(response => {
            return response.json();
          })
          .then(this.setResults);
    },
    setResults (results) {
      this.weather = results;
    },

    // Method to get todays Date 
    getCurrentDate() {
      const today = new Date();
      const day = today.getDate();
      const month = today.getMonth() + 1; // Months are based on 0
      const year = today.getFullYear();

      // Format (z.B. 01.11.2023)
      const formattedDate = `${day.toString().padStart(2, '0')}.${month.toString().padStart(2, '0')}.${year}`;
      
      return formattedDate;
    },

    getBackgroundClass() {
    if (typeof this.weather.main != 'undefined') {
      const temp = this.weather.main.temp;
      if (temp <= 0) {
        return 'verycold';
      } else if (temp > 0 && temp <= 11) {
        return 'cold';
      } else if (temp > 11 && temp <= 21) {
        return 'medium';
      } else if (temp > 21 && temp <= 30) {
        return 'warm';
      } else {
        return 'verywarm';
      }
    } else {
      return '';
    }
  }
}, 
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: 'arial', sans-serif;
}

#app {
  background-image: url('./assets/medium-bg.jpg');
  background-size: cover;
  background-position: bottom;
  transition: 0.4s;
}
#app.verycold {
  background-image: url('./assets/verycold-bg.jpg');
}
#app.cold {
  background-image: url('./assets/cold-bg.jpg');
}

#app.warm {
  background-image: url('./assets/warm-bg.jpg');
}

#app.verywarm {
  background-image: url('./assets/verywarm-bg.jpg');
}

main {
  min-height: 100vh;
  padding: 25px;
}

.search-box {
  width: 100%;
  margin-bottom: 30px;
}

.search-box .search-bar {
  display: block;
  width: 100%;
  padding: 15px;
  
  color: #313131;
  font-size: 20px;

  appearance: none;
  border:none;
  outline: none;
  background: none;

  box-shadow: 0px 0px 8px rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.5);
  border-radius: 0px 16px 0px 16px;
  transition: 0.4s;
}

.search-box .search-bar:focus {
  box-shadow: 0px 0px 16px rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.75);
  border-radius: 16px 16px 16px 16px;
}

.location-box .location {
  color: #FFF;
  font-size: 32px;
  font-weight: 500;
  text-align: center;
  text-shadow: 1px 3px rgba(0, 0, 0, 0.25);
}

.location-box .date {
  color: #FFF;
  font-size: 20px;
  font-weight: 300;
  font-style: italic;
  text-align: center;
}

.weather-box {
  text-align: center;
}

.weather-box .temp {
  display: inline-block;
  padding: 10px 25px;
  color: #FFF;
  font-size: 102px;
  font-weight: 900;

  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
  background-color:rgba(255, 255, 255, 0.25);
  border-radius: 16px;
  margin: 30px 0px;

  box-shadow: 3px 6px rgba(0, 0, 0, 0.25);
}

.weather-box .weather {
  color: #FFF;
  font-size: 48px;
  font-weight: 700;
  font-style: italic;
  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
}

.intro-message {
  font-size: 48px;
  font-weight: 700;
  font-style: italic;
  text-align: center;

  display: inline-block;
  padding: 10px 25px;
  color: #ffffff;

  background-color:rgba(255, 255, 255, 0.5);
  border-radius: 16px;
  margin: 30px 0px;
}
</style>
