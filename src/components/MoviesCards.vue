<template>
  <div class="container grid gap-3 mx-auto my-3 text-center lg:grid-cols-2 mt-20">
      <Card v-for="(movie,index) in movies" :key="index" :movie="movie" />
  </div>
</template>

<script setup>
  import { onMounted } from 'vue'
  import { getMovies, movies, page } from '~/helpers/useMovies'

  onMounted(() => {
    getMovies()
  })
</script>
