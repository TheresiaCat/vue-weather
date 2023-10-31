<template>
  <div id="app">
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

</style>
