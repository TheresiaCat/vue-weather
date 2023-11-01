<template>
  <div id="app">
    <main>
      <!--Searchbox-->
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
      <div class="weather-wrap">
        <div class="location-box">
          <div class="location">Mosbach, DE</div>
          <div class="date">01.11.2023</div>
      </div>  
      </div>

      <!--Weather Information-->
      <div class="weather-box">
          <div class="temp">20°c</div>
          <div class="weather">Sunshine</div>
    </div>
    </main>
  </div>
</template>

<script>
export default {
  name: 'App', 
  
  //Gibt Objekt zurück mit den Daten von der API
  data () {
    return {
      api_key: '87ecc09b44dd66f2699a03e91094bc23',
      url_base: 'https://api.openweathermap.org/data/2.5/',
      query: '',
      weather: {}
    }
  }
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
  background-image: url('./assets/cold-bg.jpg');
  background-size: cover;
  background-position: bottom;
  transition: 0.4s;
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
</style>
