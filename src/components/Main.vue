<template>
  <div class="container">
    <ul>
      <li>{{ town }}</li>
      <li>{{ weather }}</li>
      <li>{{ sunrise }}</li>
      <li>{{ sunset }}</li>
    </ul>
    <button v-on:click="hello"></button>
    <button v-on:click="convert"></button>
  </div>
</template>

<script>
import axios from 'axios'
import key from '../config.js';

export default {
  name: 'Main',
  props: {
    msg: String
  },
  data() {
    return {
      info: '',
      town: '',
      response: '',
      sunrise: '',
      sunset: '',
      weather: ''
    }
  },
  mounted() {
    const api = key.api_key;
    axios.get(`https://api.openweathermap.org/data/2.5/weather?zip=12721,us&APPID=`+`${api}`)
        .then((response) => {
          this.info = response;
          this.town = response.data.name;
          this.sunrise = response.data.sys.sunrise;
          this.sunset = response.data.sys.sunset;
          this.weather = response.data.weather[0].main;
          console.log(response);
        })
        .catch((err) => {
          console.log(err);
        });
  },
  methods: {
    hello() {
      alert('hi');
    },
    convert() {
      alert('convert')
    }
  }
}



/*
It is easy to convert Kelvin to Fahrenheit with these four steps.

Subtract 273.15 from your Kelvin temperature
Multiply this number by 1.8 (this is the decimal value of 9/5).
Add 32 to this number.

*/


</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .container {
    border: 2px solid red;
  }
</style>
