<template>
  <div class="container">
    <h1>Weather</h1>
    <ul>
      <li>Town: {{ town }}</li>
      <li>Forecast: {{ forecast }}</li>
      <li>Sunrise: {{ sunrise }}</li>
      <li>Sunset: {{ sunset }}</li>
      <li><img :src="`https://openweathermap.org/img/w/${iconCode}.png`"/></li>
    </ul>
    <br/>
    <!--<img :src="logo"/>-->
    <button v-on:click="hello"></button>
    <button v-on:click="convert"></button>
  </div>
</template>

<script>
import axios from 'axios'
import key from '../config.js'
import logo from '../assets/logo.png'

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
      forecast: '',
      iconCode: '',
      logo: logo
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
          this.forecast = response.data.weather[0].main;
          this.iconCode = response.data.weather[0].icon;
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
    convert(temp) {
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
    background: #222930;
    color: #E9E9E9;
  }

  ul {
    list-style-type: none;
    display: inline-block;
  }

  ul li {
    color: #4EB1BA;
    display: inline;
    margin: .5em;
  }

  /* #222930
    #4EB1BA
    #E9E9E9
  */
</style>
