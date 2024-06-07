<template>
  <div class="flex flex-1">
    <div>
      <TemplateView/>
    </div>
    <main class="flex-1">
      <div class="flex bg-gray-100 pb-24 pt-5 sm:pb-32">
        <div class="mx-auto max-w-7xl px-6 text-center lg:px-8">
          <div class="mx-auto max-w-2xl">
            <h2 class="text-3xl font-bold tracking-tight text-black sm:text-4xl">Tracks</h2>
            <p class="mt-4 text-lg leading-8 text-gray-600">
              This is the Tracks page. Here you can view all the tracks in DreamSreamer.
            </p>
          </div>

          <ul role="list" class="mx-auto mt-20 grid max-w-2xl grid-cols-1 gap-6 sm:grid-cols-2 lg:mx-0 lg:max-w-none lg:grid-cols-3 lg:gap-8">
            <li v-for="track in tracks" :key="track.id" class="rounded-2xl bg-gray-200 px-8 py-10">
              <RouterLink :to="`/tracks/${track.id}`">
                
              <img class="mx-auto h-48 w-48 rounded-full md:h-56 md:w-56" :src="track.avatar" alt="track image" />
              <h3 class="mt-6 text-base font-semibold leading-7 tracking-tight text-black">{{ track.name }}</h3>
              <p class="text-sm leading-6 text-gray-600">{{ track.artist.name }}</p>
              </RouterLink>
            </li>
          </ul>
        </div>
      </div>
    </main>
  </div>
<router-view />
</template>

<script type="module">

import { onMounted, ref } from 'vue';
import { RouterLink } from 'vue-router';
import TemplateView from '../TemplateView.vue';

export default {

  components: {
    TemplateView
  },

  setup() {

    const tracks = ref([]);
    
    onMounted(() => {
      getTracks()
    })

    function getTracks() {
      
      fetch('https://h3ofpd5s5b.execute-api.ap-southeast-1.amazonaws.com/dev/tracks')
      .then((response) => response.json())
      .then((response) => {
        console.log(response)
        tracks.value = response.body
      })
    }

    return {
      getTracks,
      tracks
    }
  }
}

</script>