// Weather.vue

<template>
  <div>
    <h1>My Weather App</h1>
    <button v-on:click="getWeatherData">Get Weather Data</button>
    <div v-for="weather in weatherDataList" :key="weather.id" class="weather-data">
    <pre>{{JSON.stringify(weather, null, 2)}}</pre>
    <div class="weather-stats">
      </div>
      <div>
          <span class="location">{{weather.id}}</span>
          <br/>
          <span class="location">{{weather.coord.lon}}</span>
          <span class="location">{{weather.weather[0].description}}</span>
        </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Weather",
  data() {
    return {
      weatherDataList: []
    };
  },
  methods: {
    getWeatherData() {
      fetch("weather.json")
        .then(response => response.json())
        .then(data => (this.weatherDataList = data));
    }
  }
};
</script>

<style scoped>

.weather-data {
  display: flex;
  align-items: center;
  margin-top: 20px;
  margin-left: 20px;
  border-bottom: 2px solid #ccc;
  padding: 20px;
}

.weather-stats {
  flex-grow: 8;
  text-align: left;
  padding-left: 20px;
}

.weather-stats .location {
  font-size: 30px;
}

button {
    padding:10px;
    background-color: #1aa832;
    color: white;
    border: 1px solid #ccc;
}
</style>