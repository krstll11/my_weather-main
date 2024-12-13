<template>
    <div class="future">
      <h1>Прогноз погоды</h1>
      <div class="cubes">
      <div v-for="item in msg?.list" :key="item.dt" class="cube">
      <p>Дата и время: {{ item.dt_txt }}</p>
      <img :src="`http://openweathermap.org/img/wn/${item.weather[0].icon}@2x.png`">
      <p>Направление ветра: </p>
      <div v-if="item.wind.deg<90 && item.wind.deg>0">Северный</div>
      <div v-else-if="item.wind.deg<180 && item.wind.deg>90">Южный</div>
      <div v-else-if="item.wind.deg<270 && item.wind.deg>180">Восточный</div>
      <div v-else>Западный</div>
      <p>Скорость ветра: {{ item.wind.speed }} м/c</p>
      <p>Температура: {{ item.main.temp }} °C</p>
      </div>
    </div>
  </div>
  </template>
  
  <script>
export default {
  name: 'FutureWeather',
  props: ['msg']
  ,
  data() {
    return {
      weatherData: null,
    };
  },
  methods : {
    },
  }

 


  </script>
  
  <style scoped>
  ul {
    list-style-type: none;
    padding: 0;
  }
  li {
    margin-bottom: 10px;
  }
  .future-weather {
  display: flex;
  flex-direction: column;
  align-items: center;
  background-color: #fafafa;
  border-radius: 10px;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
  padding: 20px;
  width: 90%;
  max-width: 600px;
  margin: 20px auto;
}

.future-weather h1 {
  font-size: 24px;
  color: #333;
  margin-bottom: 15px;
}
.cubes {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(150px, 1fr));
  gap: 12px;
  justify-items: stretch;
}
.cube{
  background-color: rgba(255, 255, 255, 0.785);
  padding: 14px;
  display: flex;
  flex-direction: column;
  gap: 8px;
  text-align: center;
  border-width: 1px;
  border-style: solid;
  border-color: black;
}
  </style>