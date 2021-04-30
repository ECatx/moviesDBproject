<template>
  <div class="flex items-center justify-center mb-5 space-x-3">
      <div v-if="page > 1">
          <button @click="prevPage" class="px-4 py-2 bg-white rounded">Previous</button>
      </div>
      <div>
          <p class="px-4 text-blueGray-200">Page {{page}} of {{pages}}</p>
      </div>
      <div>
          <button @click="nextPage" class="px-4 py-2 bg-white rounded">
              Next
          </button>
      </div>
  </div>
</template>

<script setup>
  import { page, pages, nextPage, prevPage } from '~/helpers/useMovies'
</script>
