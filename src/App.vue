<template>
  <NavBar />
  <Home v-if="isAuthenticated" class=""/>
  <EmptyHome v-else />
  <Footer v-if="isAuthenticated"/>
</template>

<script setup>
  import { authentication } from '~/helpers/useFirebase'

  const { isAuthenticated } = authentication()
</script>
