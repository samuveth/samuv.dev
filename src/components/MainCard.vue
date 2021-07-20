<template>
  <div class="w-full text-left bg-gray-400 bg-opacity-10 rounded-md px-6 py-5 text-gray-800 dark:text-gray-400 cursor-pointer ">
    <h3 class="text-xl dark:text-gray-200 mb-1.5">
      {{ title }}
    </h3>
    <span class="opacity-60 text-[1.1rem]">
      Lorem ipsum dolor.
    </span>
  </div>
</template>

<script lang="ts" setup>
defineProps(['title'])
</script>
