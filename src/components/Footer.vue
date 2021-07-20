<script setup lang="ts">

import { isDark, toggleDark } from '~/logic'

</script>

<template>
  <nav class="text-2xl mt-6 md:flex md:flex-row md:justify-start">
    <button class="icon-btn mx-2" @click="toggleDark()">
      <carbon-sun v-if="isDark" />
      <carbon-moon v-else />
    </button>

    <a class="icon-btn mx-2" rel="noreferrer" href="https://github.com/samuveth" target="_blank" title="GitHub">
      <carbon-logo-github />
    </a>
    <a class="icon-btn mx-2" rel="noreferrer" href="https://twitter.com/samuveth" target="_blank" title="GitHub">
      <mdi:twitter />
    </a>
  </nav>
</template>
