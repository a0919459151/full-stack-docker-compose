<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <h2>Weather Forecast</h2>
    <div v-if="loading">Loading...</div>
    <ul v-else>
      <li v-for="forecast in weatherForecasts" :key="forecast.date">
        Date: {{ forecast.date }}, Temperature: {{ forecast.temperatureC }}°C ({{ forecast.temperatureF }}°F), Summary: {{ forecast.summary }}
      </li>
    </ul>
  </div>
</template>

<script>
import api from '@/services/api';

export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data() {
    return {
      weatherForecasts: [],
      loading: true
    }
  },
  mounted() {
    this.fetchWeatherForecasts();
  },
  methods: {
    async fetchWeatherForecasts() {
      try {
        const response = await api.get('/WeatherForecast');
        this.weatherForecasts = response.data;
        this.loading = false;
      } catch (error) {
        console.error('Error fetching weather forecasts:', error);
        this.loading = false;
      }
    }
  }
}
</script>