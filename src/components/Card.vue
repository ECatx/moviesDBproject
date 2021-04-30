<template>
  <div class="max-w-full flex">
      <img :src="`${posterBaseURL}${movie.poster_path}`" :alt="`Poster of ${movie.title}`">
      <div class="flex flex-col justify-between p-4 leading-normal bg-white border-b border-l border-r border-blueGray-400 rounded-b lg:border-l-0 lg:border-t lg:border-blueGray-400 lg:rounded-b-none lg:rounded-r">
          <div class="mb-8">
              <div class="mb-2 text-xl font-semibold text-blueGray-900">
                  {{movie.title}}
              </div>
              <p class="text-base text-blueGray-700 line-clamp-6">
                  {{movie.overview}}
              </p>
          </div>
          <div class="flex items-start justify-end">
              <div class="flex flex-col items-center">
                  <button class="text-blueGray-700 hover:text-rose-600" @click="newLike"> 
                      <mdi:heart-plus class="w-8 h-8"/>
                      <span>{{likes}}</span>
                  </button>
              </div>
              <div class="flex flex-col items-center pl-2">
                  <button  class="text-blueGray-700 hover:text-green-400" @click="toggle">
                      <bx:bxs-comment-add class="w-8 h-8" />
                  </button>
              </div>
          </div>
      </div>
  </div>
  <Comments v-if="value" @close="toggle" :movie="movie"/>
</template>
<script setup>
  import { defineProps, ref, onMounted, toRefs, watch } from 'vue'
  import { useToggle } from '@vueuse/core'

  import { posterBaseURL } from '~/helpers/useMovies'
  import { countByObjectId, add } from '~/helpers/useLikes'
  import { authentication } from '~/helpers/useFirebase'

  const [value, toggle] = useToggle(false)

  const { user } = authentication()

  const props = defineProps({
    movie: {
      type: Object,
      default: () => {
        return {
          title: '',
          overview: '',
          poster_path: '',
          id: '',
        }
      },
    },
  })

  const newLike = async () => {
    await add({ objectId: props.movie.id.toString(), userId: user.value.uid })
    await getLikes()
  }

  const likes = ref(0)

  const getLikes = async () => {
    const response = await countByObjectId(props.movie.id.toString())
    const { data } = response
    if (data) likes.value = data.count
  }

  onMounted(() => {
    getLikes()
  })

  const { movie } = toRefs(props)

  watch(movie, () => {
    getLikes()
  })
</script>
