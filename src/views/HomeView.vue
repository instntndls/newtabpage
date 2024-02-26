<script setup>

import SearchBar from "@/components/SearchBar.vue";
import Favorites from "@/components/Favorites.vue";
</script>

<template>
  <img class="w-screen h-screen absolute object-cover blur-2xl opacity-80 brightness-50 select-none" src="/src/assets/background.jpg" alt="Backdrop">
  <div class="Frame flex flex-col w-screen h-screen items-center justify-center gap-8">
    <SearchBar />
    <Favorites />

  </div>

</template>

<style>

</style>