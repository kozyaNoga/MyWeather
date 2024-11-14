<template>
  <!DOCTYPE html>
  <html lang="en">
    <head>
      efdfd
    </head>
    <body>
      <header>
        <h1>Приложение погоды</h1>
      </header>
      <main>
        <select @change="select_city" v-model="selectedCity">
          <option v-for="(c,i) in city" :value="i" :key="i">{{ c.name }}</option>
        </select>
        <p v-if="!weather_data">Загрузка...</p> 
        <div v-if="forecast_data" class="cards">
          <ForecastCard
            v-for="(f, i) in forecast_data.list"
            :key="i"
            :forecast_data="f">
            
          </ForecastCard>
        </div>
      </main>
      <footer>

      </footer>
    </body>
  </html>
</template>

<script>
import ForecastCard from './components/ForecastCard.vue';

export default {
  name: 'App',
  data(){
    return {
      forecast_data: null,
      weather_data: null,
      selectedCity: null,
      selectInfo: 'temp',
      city: [
        {name: 'Нижний Тагил', lat: '57.91', lon:'59.96'},
        {name: 'Сочи', lat: '43.60', lon:'39.72'},
        {name: 'Усть-кут', lat: '56.78', lon:'105.74'},
        {name: 'Норильск', lat: '69.35', lon:'88.20'}
      ]
    }
  },
  mounted(){
    this.selectedCity=0;
    this.select_city();
  },
  methods:{
    select_city(){
    //fetch(`https://api.openweathermap.org/data/2.5/weather?lat=${this.city[this.selectedCity].lat}&lon=${this.city[this.selectedCity].lon}&appid=d5cf04b5ad87f65ba02070c805dcad72&units=metric&lang=ru`)
    fetch('weather.json')
    .then(resp=>resp.json())
    .then(json=>{
      this.weather_data=json;
    });

    //fetch(`https://api.openweathermap.org/data/2.5/forecast?lat=${this.city[this.selectedCity].lat}&lon=${this.city[this.selectedCity].lon}&appid=d5cf04b5ad87f65ba02070c805dcad72&units=metric&lang=ru`)
    //api.openweathermap.org/data/2.5/forecast/daily?lat=${this.city[this.selectedCity].lat}&lon=${this.city[this.selectedCity].lon}&cnt=5&appid=d5cf04b5ad87f65ba02070c805dcad72&units=metric&lang=ru
    fetch('forecast.json')
    .then(resp=>resp.json())
    .then(json=>{
      this.forecast_data=json;
    });
    }
  },
  components: { 
    ForecastCard
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
  margin-top: 0px;
}
.cards{
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  gap: 10px;
  justify-content: center;
  
}
main{
  padding: 0pt 0pt 0pt 0pt;
  margin: 0pt 20% 0pt 20%;
}
select{
  margin: 5% 0% 5% 0%;
  min-width: 20%;
  min-height: 10%;
  font-size: 15pt;
}
header{
  background-color: black;
  color: azure;
  margin: 0pt 0pt 0pt 0pt;
  padding: 10pt 0pt 10pt 0pt;
}
body{
  margin: 0pt 0pt 0pt 0pt;
  padding: 0pt 0pt 0pt 0pt;
}
</style>
