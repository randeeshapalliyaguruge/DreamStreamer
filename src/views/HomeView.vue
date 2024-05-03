<script setup>
import { ref } from 'vue'
import TemplateView from './TemplateView.vue';

const count = ref(0)
</script>

<template>
  <div class="flex flex-1">
    <div>
    <TemplateView/>
    </div>
    <div class="flex-1" v-on:click="count++">
      Hello from home

      {{ count }}
    </div>
  </div>
</template>
