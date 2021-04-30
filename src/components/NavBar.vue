<template>
  <nav class="bg-gray-800 fixed top-0 left-0 right-0 py-2">
      <div class="container mx-auto flex items-center justify-between shadow-xl">
          <div class="flex items-center space-x-5">
              <whh:movieclapper class="h-12 w-12 text-coolGray-500"/>
              <p class="text-4xl tracking-widest text-transparent font-light bg-clip-text bg-gradient-to-r from-rose-500 via-green-600 to-blue-700">Movies<span class="font-bold">DB</span></p>
          </div>
          <div>
              <div v-if="isAuthenticated" class="flex items-center space-x-5">
                <p class="text-blueGray-400">Hello {{user?.displayName}}</p>
                <button class="px-8 py-2 font-medium bg-purple-900 rounded-full focus:ring-pink-400 focus:ring-2 focus:outline-none text-blueGray-300 hover:bg-purple-700" @click="out">
                  Logout
              </button> 
              </div>
              <div v-else>
                  <button class="px-8 py-2 font-medium bg-blue-900 rounded-full focus:ring-yellow-400 focus:ring-2 focus:outline-none text-blueGray-300 hover:bg-blue-700" @click="signIn">
                      Login
                  </button>
              </div>
          </div>
      </div>
  </nav>
</template>


<script setup>
  import { authentication } from '~/helpers/useFirebase'
  import { movies, page } from '~/helpers/useMovies'

  const { signIn, signOut, isAuthenticated, user } = authentication()

  const out = () => {
    signOut()
    page.value = 1
    movies.value = []
  }
</script>
