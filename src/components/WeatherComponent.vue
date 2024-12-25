<script setup>
import { ref } from 'vue'
import axios from 'axios'
// import warmBg from '@/assets/warm-bg-png'
// import coldBg from '@/assets/cold-bg-png'

const backgroundImage = ref('background')

const city = ref('')
const weatherData = ref(null)

const API_KEY = 'c4ace96d18cb613288964e252738b47b'

const fetchWeather = async (event) => {
  if (event.key === 'Enter') {
    try {
      const response = await axios.get('https://api.openweathermap.org/data/2.5/weather', {
        params: {
          appid: API_KEY,
          q: city.value,
          units: 'metric'
        }
      })
      console.log(weatherData)
      weatherData.value = response.data
      city.value = ''

      if (response.data.main.temp > 17) {
        backgroundImage.value = 'warm-background'
      } else {
        backgroundImage.value = 'cold-background'
      }
    } catch (error) {
      console.error('Error in fetching weather data', error)
    }
  }
}

const dateBuilder = () => {
  let d = new Date()
  let months = [
    'January',
    'February',
    'March',
    'April',
    'May',
    'June',
    'July',
    'August',
    'September',
    'October',
    'November',
    'December'
  ]
  let days = ['Sunday', 'Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday']

  let day = days[d.getDay()]
  let date = d.getDate()
  let month = months[d.getMonth()]
  let year = d.getFullYear()

  return `${day} ${date} ${month} ${year}`
}
</script>

<template>
  <div class="weather-container" :class="[backgroundImage]">
    <div class="overlay">
      <div class="search-box">
        <input
          type="text"
          class="cityInput"
          placeholder="search city here..."
          v-model="city"
          @keypress="fetchWeather"
        />
      </div>
      <div class="weather-info" v-if="weatherData">
        <div class="city-name">{{ weatherData.name }}, {{ weatherData.sys.country }}</div>
        <div class="date">{{ dateBuilder() }}</div>
        <div class="temperature">
          <div class="temp-overlay">{{ Math.round(weatherData.main.temp) }}°c</div>
        </div>
        <div class="weather">{{ weatherData.weather[0].description }}</div>
      </div>
      <div v-else>
        <p class="weather-info">Enter a city to get the weather information.</p>
      </div>
    </div>
  </div>
</template>

<style lang="scss" scoped>
// .background {
//   background-image: url(../assets/warm-bg.png);
// }

// .warm-background {
//   background-image: url(../assets/warm-bg.png);
// }

// .cold-background {
//   background-image: url(../assets/cold-bg.png);
// }

.weather-container {
  background-image: url(../assets/cold-bg.png);
  transition: background-image 0.5s ease-in-out; /* Smooth transition when switching images */

  height: 100vh;

  .overlay {
    background-color: rgba($color: #000000, $alpha: 0.5);
    height: 100%;
    padding: 25px;
  }

  .search-box {
    width: 100%;
    text-align: center;
    margin-top: 3rem;

    input {
      height: 3rem;
      padding-left: 1rem;
      width: calc(100% - 5rem);
      border-radius: 10px;
      box-shadow: 0px 0px 5px rgba($color: #000000, $alpha: 0.3);
      font-size: 1.15rem;
      transition: 0.2s ease-in-out;

      &:focus {
        outline: none;
        background-color: rgba($color: #000000, $alpha: 0.9);
        color: white;
      }
    }
  }

  .weather-info {
    display: grid;
    place-items: center;
    margin: 2rem auto;
    color: white;

    .city-name {
      font-size: 3rem;
      font-weight: 600;
      color: white;
      text-shadow: 1px 3px rgba($color: #000000, $alpha: 0.25);
    }

    .date {
      font-size: 1.15rem;
      font-style: italic;
      font-weight: 500;
      text-shadow: 1px 3px rgba($color: #000000, $alpha: 0.15);
    }

    .temperature {
      font-size: 7rem;
      font-weight: 700;

      .temp-overlay {
        background-color: rgba($color: #ded3d3, $alpha: 0.3);
        border-radius: 10px;
        margin-top: 1rem;
        padding: 0rem 2rem;
      }
    }

    .weather {
      font-size: 2rem;
      font-style: italic;
      font-weight: 500;
      text-shadow: 1px 3px rgba($color: #000000, $alpha: 0.15);
    }
  }
}
</style>
