<script setup>
import { ref } from 'vue'
import axios from 'axios'

const movie = ref('')
const movieData = ref(null)

const API_key = '3a1569eb'

const searchMovie = async (event) => {
  if (event.key === 'Enter') {
    try {
      const response = await axios.get('http://www.omdbapi.com/', {
        params: {
          apikey: API_key,
          s: movie.value
        }
      })

      //   if(response.data.Response === 'True') {
      //     movieData.value = response.data.Search
      //   } else {
      //     movieData.value = null
      //     console.error('Could not get movie data')
      //   }
      movieData.value = response.data.Search
      console.log(movieData)

      movie.value = ''
    } catch (error) {
      console.error('Error in fetching the movie Info', error)
    }
  }
}
</script>

<template>
  <div class="grid place-items-center bg-blue-50">
    <div class="grid place-items-center p-5 bg-white w-full">
      <input
        type="text"
        placeholder="search movie here..."
        v-model="movie"
        @keypress="searchMovie"
        class="border rounded-lg p-2 focus:outline-none focus:ring-2 w-80 focus:ring-emerald-400"
      />
    </div>
    <div
      v-if="movieData"
      class="grid place-items-center border p-3 w-full sm:grid sm:grid-cols-2 sm:justify-evenly md:grid-cols-3"
    >
      <div v-for="movie in movieData" :key="movie.imdbID">
        <div class="movie-data border-2 p-3 w-80 md:w-auto md:min-w-60 lg:w-80 my-3 bg-white">
          <div class="poster w-full">
            <img :src="movie.Poster" class="w-full h-80 object-cover" :alt="movie.Title" />
          </div>
          <div class="title font-semibold text-lg text-left w-full">{{ movie.Title }}</div>
          <div class="flex justify-between items-center mt-2">
            <div class="year font-semibold text-gray-500">{{ movie.Year }}</div>
            <div class="type border-2 p-1 font-semibold">{{ movie.Type }}</div>
          </div>
        </div>
      </div>
    </div>
    <div v-else class="text-gray-500 bg-white w-full text-center">
      Enter the movie title to get the information
    </div>
  </div>
</template>
