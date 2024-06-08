<template>
  <div class="flex flex-1">
    <div>
      <TemplateView/>
    </div>
    <main class="flex-1">
      <div class="flex bg-gray-100 pb-24 pt-5 sm:pb-32">
        <div class="mx-auto max-w-7xl px-6 text-center lg:px-8">
          <div class="mx-auto max-w-2xl">
            <h2 class="text-3xl font-bold tracking-tight text-black sm:text-4xl">Albums</h2>
            <p class="mt-4 text-lg leading-8 text-gray-600">
              This is the Albums page. Here you can view all the albums in DreamSreamer.
            </p>
          </div>
          
          <div class="flex gap-2 items-end mt-5">
            <!-- <label for="year" class="block text-lg font-medium text-gray-700">Select Year</label> -->
            <select 
              v-model="year"
              id="year" name="year" class="mt-1 block
              w-full pl-3 pr-10 py-2 text-base border-gray-300 focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm rounded-md">
              <option value="" selected>Select Year</option>
              <option value="2005">2005</option>
              <option value="2012">2012</option>
              <option value="2016">2016</option>
            </select>

            <button type="button" @click="getAlbums" class="mt-2">
              FILTER
            </button>

          </div>

          
          <ul role="list" class="mx-auto mt-20 grid max-w-2xl grid-cols-1 gap-6 sm:grid-cols-2 lg:mx-0 lg:max-w-none lg:grid-cols-3 lg:gap-8">
            <li v-for="album in albums" :key="album.id" class="rounded-2xl bg-gray-200 px-8 py-10">
              <RouterLink :to="`/${album.id}`">
                
              <img class="mx-auto h-48 w-48 rounded-full md:h-56 md:w-56" :src="album.album_art" alt="album_art" />
              <h3 class="mt-6 text-base font-semibold leading-7 tracking-tight text-black">{{ album.name }}</h3>
              <p class="text-sm leading-6 text-gray-600">{{ album.year }}</p>
              <ul role="list" class="mt-6 flex justify-center gap-x-6">
                <li>
                  <a :href="album.xUrl" class="text-gray-600 hover:text-gray-500">
                    <span class="sr-only">X</span>
                    <svg class="h-5 w-5" aria-hidden="true" fill="currentColor" viewBox="0 0 20 20">
                      <path d="M11.4678 8.77491L17.2961 2H15.915L10.8543 7.88256L6.81232 2H2.15039L8.26263 10.8955L2.15039 18H3.53159L8.87581 11.7878L13.1444 18H17.8063L11.4675 8.77491H11.4678ZM9.57608 10.9738L8.95678 10.0881L4.02925 3.03974H6.15068L10.1273 8.72795L10.7466 9.61374L15.9156 17.0075H13.7942L9.57608 10.9742V10.9738Z" />
                    </svg>
                  </a>
                </li>
                <li>
                  <a :href="album.linkedinUrl" class="text-gray-600 hover:text-gray-500">
                    <span class="sr-only">LinkedIn</span>
                    <svg class="h-5 w-5" aria-hidden="true" fill="currentColor" viewBox="0 0 20 20">
                      <path fill-rule="evenodd" d="M16.338 16.338H13.67V12.16c0-.995-.017-2.277-1.387-2.277-1.39 0-1.601 1.086-1.601 2.207v4.248H8.014v-8.59h2.559v1.174h.037c.356-.675 1.227-1.387 2.526-1.387 2.703 0 3.203 1.778 3.203 4.092v4.711zM5.005 6.575a1.548 1.548 0 11-.003-3.096 1.548 1.548 0 01.003 3.096zm-1.337 9.763H6.34v-8.59H3.667v8.59zM17.668 1H2.328C1.595 1 1 1.581 1 2.298v15.403C1 18.418 1.595 19 2.328 19h15.34c.734 0 1.332-.582 1.332-1.299V2.298C19 1.581 18.402 1 17.668 1z" clip-rule="evenodd" />
                    </svg>
                  </a>
                </li>
              </ul>
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
import TemplateView from './TemplateView.vue';

export default {

  components: {
    TemplateView
  },

  setup() {

    const albums = ref([]);
    const year = ref("");
    
    onMounted(() => {
      getAlbums()
    })

    function getAlbums() {
      
      fetch('https://h3ofpd5s5b.execute-api.ap-southeast-1.amazonaws.com/dev/albums?year=' + year.value)
      .then((response) => response.json())
      .then((response) => {
        console.log(response)
        albums.value = response.body
      })
    }

    return {
      getAlbums,
      year,
      albums
    }
  }
}

</script>