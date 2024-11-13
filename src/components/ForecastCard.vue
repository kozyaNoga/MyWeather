<template>
    <div class="card">
        <img :src="`http://openweathermap.org/img/wn/${forecast_data.weather[0].icon}@2x.png`">
        <p>Дата и время: {{ forecast_data.dt_txt }}</p>
        <p>Температура: {{ forecast_data.main.temp }}</p>
        <p>Давление: {{ forecast_data.main.pressure }}</p>
        <p>Влажность: {{ forecast_data.main.humidity }}</p>
        <p>Описание погоды: {{ forecast_data.weather[0].description }}</p>
    </div>
</template>

<script>
export default{
    name: "ForecastCard",
    props:{
        forecast_data:{
            type:Object
        }
    },
}
</script>

<style scoped>
    .card{
        width: 200px;
        min-height: 50px;
        border: 1px solid black;
    }
</style>