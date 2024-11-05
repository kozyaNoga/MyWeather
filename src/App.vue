<template>
  <h1>Приложение погоды</h1>
  <select @change="select_city" v-model="selectedCity">
  <option v-for="(c,i) in city" :value="i" :key="i">{{ c.name }}</option>
  </select>
  <p v-if="!weather_data">Загрузка...</p> 
  <div v-else>
    <p>Температура: {{ weather_data.main.temp }}</p>
    <p>Давление: {{ weather_data.main.pressure }}</p>
    <p>Облачность: {{ weather_data.weather.description }}</p>
    <p>Уровень моря: {{ weather_data.main.sea_level }}</p>
  </div>
</template>

<script>
export default {
  name: 'App',
  data(){
    return {
      weather_data: null,
      selectedCity: null,
      selectInfo: 'temp',
      city: [
        {name: 'Нижний Тагил', lat: '57.55', lon:'59.58'},
        {name: 'Сочи', lat: '23.55', lon:'51.58'},
        {name: 'Усть-кут', lat: '51.55', lon:'29.58'},
        {name: 'Норильск', lat: '51.55', lon:'29.58'}
      ]
    }
  },
  mounted(){
    this.selectedCity=0;
    this.select_city();
  },
  methods:{
    select_city(){
    fetch(`https://api.openweathermap.org/data/2.5/weather?lat=${this.city[this.selectedCity].lat}&lon=${this.city[this.selectedCity].lon}&appid=d5cf04b5ad87f65ba02070c805dcad72&units=metric&lang=ru`)
    .then(resp=>resp.json())
    .then(json=>{
      this.weather_data=json;
    });
    }
  },
  components: { 

  },
}
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
