<template>
  <div id="app">
    <FutureWeather :msg="weather_future"/>
  </div>
  <h1>Приложение погоды</h1>
  <div сlass="main-weather">
    <p>Температура: {{weather_data?.main.temp}} °C</p>
    <p>Влажность: {{weather_data?.main.humidity}}</p>
    <p>Давление: {{weather_data?.main.pressure}}</p>
    <p>Ветер: {{weather_data?.wind.speed}} м/c</p>
    <p>Видимость: {{weather_data?.visibility}} м</p>
    <p>Облачность: {{weather_data?.clouds.all}}</p>
    <p>Город:{{ weather_data?.name }}</p>
  </div>
  <button @click="getWeatherFuture">Погода на неделю</button>
  <select v-model="selectedCity" @change="getWeatherData(selectedCity)">
    <option v-for="city in Object.keys(city)" :key="city" :value="city">{{ city }}</option>
  </select>
</template>

<script>
import FutureWeather from './components/FutureWeather.vue';

export default {
  name: 'App',
  components: {
    FutureWeather,
  },
  data(){
    return {
      weather_data:null,
      weather_future: null,
      city: {
        "Нижний Тагил": [57.9194, 59.965],
        "Москва": [55.7558, 37.6176],
        "Санкт-Петербург": [59.9391, 30.3151],
        "Сочи": [43.5889, 39.7244],
        "Монреаль": [45.5089, -73.5617],
        "Балтимор": [42.9, -73.1],
        "Нью-Джерси": [40.7143, -74.006],
      },
      selectedCity: "Москва",
      APIkey : "c4292fb2990492b78f88e9413b3ac7c2&units=metric",
    }
   
  },
  mounted() {
    fetch(`https://api.openweathermap.org/data/2.5/weather?lat=57.9194&lon=59.965&appid=${this.APIkey}`)
    
    .then(resp => resp.json())
    .then(data =>{this.weather_data = data;});
  },
  methods : {
    getWeatherData() {
      fetch(`https://api.openweathermap.org/data/2.5/weather?lat=${this.city[this.selectedCity][0]}&lon=${this.city[this.selectedCity][1]}&appid=${this.APIkey}`)
      .then(resp => resp.json())
      .then(data =>{this.weather_data = data;});
    },
    getWeatherFuture() {
      fetch(`https://api.openweathermap.org/data/2.5/forecast?lat=${this.city[this.selectedCity][0]}&lon=${this.city[this.selectedCity][1]}&appid=${this.APIkey}`)
      .then(resp => resp.json())
      .then(data =>{this.weather_future = data;});
  },
    
}}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
