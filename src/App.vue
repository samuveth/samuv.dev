<script setup lang="ts">
import { useHead } from '@vueuse/head'

// https://github.com/vueuse/head
// you can use this to manipulate the document head in any components,
// they will be rendered correctly in the html results with vite-ssg
useHead({
  title: 'Samuel Vallon | Frontend developer',
  meta: [
    { name: 'description', content: 'This is my developer portfolio.' },
  ],
})
</script>

<template>
  <router-view />
</template>

<style>
@import url('https://fonts.googleapis.com/css2?family=Raleway:wght@100;300;400;500;600;700;800;900&display=swap');

* {
font-family: 'Raleway', sans-serif;
}
</style>
