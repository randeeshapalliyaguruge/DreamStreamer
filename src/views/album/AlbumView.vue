<template>
    <div class="flex flex-1">
      <div>
        <TemplateView/>
      </div>
      <main class="flex-1">
        <div class="flex max-w-7xl mx-auto py-6 sm:px-6 lg:px-8">
          <div class="px-4 py-6 sm:px-0">
            <h1 class="text-2xl font-semibold text-gray-900">Albums</h1>
            <ul class="grid grid-cols-1 gap-6 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 mt-6">
              <!-- <li v-for="album in albums" :key="album.id" class="col-span-1 flex flex-col text-center bg-white rounded-lg shadow divide-y divide-gray-200">
                <div class="flex-1 flex flex-col p-8">
                  <img class="w-32 h-32 flex-shrink-0 mx-auto bg-black rounded-full" :src="album.album_art" alt="">
                  <h3 class="mt-6 text-gray-900 text-sm font-medium">{{ album.name }}</h3>
                  <dl class="mt-1 flex-grow flex flex-col justify-between">
                    <dd class="text-gray-500 text-sm">{{ album.artist.name }}</dd>
                    <dd class="text-gray-500 text-sm">{{ album.year }}</dd>
                  </dl>
                </div>
                <div class="flex-1 flex flex-col p-6">
                  <RouterLink
                    type="button"
                    class="mt-3 inline-flex w-full justify-center rounded-md bg-white px-3 py-2 text-sm font-semibold text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 hover:bg-gray-50"
                    :to="{ name: 'album.view', params: { id: album.id } }">
                    View
                  </RouterLink>
                </div>
              </li> -->
            </ul>
          </div>
        </div>
      </main>
    </div>
  </template>
  
 <script setup>
  import { ref } from 'vue';
  import { RouterLink } from 'vue-router';
  import TemplateView from '../TemplateView.vue';
  const open = ref(true)
  const albums = ref([
    {
      id: 1,
      name: 'Album 1',
      artist: {
        name: 'Artist 1',
      },
      year: 2021,
      album_art: 'https://via.placeholder.com/150',
    },
    {
      id: 2,
      name: 'Album 2',
      artist: {
        name: 'Artist 2',
      },
      year: 2020,
      album_art: 'https://via.placeholder.com/150',
    },
    {
      id: 3,
      name: 'Album 3',
      artist: {
        name: 'Artist 3',
      },
      year: 2019,
      album_art: 'https://via.placeholder.com/150',
    },
  ]);
</script>
  