<template>
  <TransitionRoot as="template" :show="open">
    <Dialog as="div" class="relative z-10" @close="open = true">
      <TransitionChild
        as="template"
        enter="ease-out duration-300"
        enter-from="opacity-0"
        enter-to="opacity-100"
        leave="ease-in duration-200"
        leave-from="opacity-100"
        leave-to="opacity-0">
        <div class="fixed inset-0 bg-gray-500 bg-opacity-75 transition-opacity" />
      </TransitionChild>

      <div class="fixed inset-0 z-10 w-screen overflow-y-auto">
        <div
          class="flex min-h-full items-end justify-center p-4 text-center sm:items-center sm:p-0">
          <TransitionChild
            as="template"
            enter="ease-out duration-300"
            enter-from="opacity-0 translate-y-4 sm:translate-y-0 sm:scale-95"
            enter-to="opacity-100 translate-y-0 sm:scale-100"
            leave="ease-in duration-200"
            leave-from="opacity-100 translate-y-0 sm:scale-100"
            leave-to="opacity-0 translate-y-4 sm:translate-y-0 sm:scale-95">
            <DialogPanel
              class="relative transform overflow-hidden rounded-lg bg-white px-4 pb-4 pt-5 text-left shadow-xl transition-all sm:my-8 sm:w-full sm:max-w-lg sm:p-6">
              <div>
                <RouterLink to="/admin/album">
                    <XMarkIcon class="h-6 w-6 text-gray-400 absolute top-4 right-4 cursor-pointer hover:bg-red-500 hover:text-white hover:rounded-full" />
                  </RouterLink>
                <div class="mt-3 sm:mt-5">
                  <DialogTitle as="h3" class="text-base font-semibold leading-6 text-gray-900">
                    {{ album.id }}. {{ album.name }}
                  </DialogTitle>
                  <div class="mt-2">
                    <div class="text-sm text-gray-500">
                      <ul>
                        <li>Number of tracks: {{ album.number_of_tracks }}</li>
                        <li>Year: {{ album.year }}</li>
                        <li>Album Art: <img :src="album.album_art" alt="Album image"></li>
                        <li>Artist: {{ album.artist ? album.artist.name : 'Loading...' }}</li>
                        <li>Studio: {{ album.studio }}</li>
                        <li>Genre: {{ album.genre }}</li>
                        <li>Sort order: {{ album.sort_order }}</li>
                        <li>Status: {{ album.status }}</li>
                      </ul>
                    </div>
                  </div>
                </div>
              </div>
              <div class="mt-5 sm:mt-6">
                <RouterLink
                  type="button"
                  class="mt-3 inline-flex w-full justify-center rounded-md bg-white px-3 py-2 text-sm font-semibold text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 hover:bg-gray-50 sm:col-start-1 sm:mt-0"
                  to="/admin/album"
                  ref="cancelButtonRef">
                  Close
                </RouterLink>
              </div>
            </DialogPanel>
          </TransitionChild>
        </div>
      </div>
    </Dialog>
  </TransitionRoot>
</template>

<script setup>
import { ref } from 'vue'
import { Dialog, DialogPanel, DialogTitle, TransitionChild, TransitionRoot } from '@headlessui/vue'
import { XMarkIcon } from '@heroicons/vue/20/solid';
import { useRoute, RouterLink } from 'vue-router'

const route = useRoute()


const open = ref(true)
const album = ref([]);

fetch('https://h3ofpd5s5b.execute-api.ap-southeast-1.amazonaws.com/dev/albums?id='+route.params.id)
  .then((response) => response.json())
  .then((response) => {
    console.log(response)
    album.value = response.body[0]
  })

// const album = {
//   id: 1,
//   name: 'Paata',
//   number_of_tracks: 8,
//   year: 2020,
//   album_art: 'IMAGE_URL',
//   artist: {
//     id: 1,
//     name: 'Costa',
//     avatar: 'IMAGE_URL'
//   },
//   studio: 'COSTA Songs',
//   genre: 'RAP',
//   sort_order: 0,
//   status: true // Published etc.
// }

</script>
