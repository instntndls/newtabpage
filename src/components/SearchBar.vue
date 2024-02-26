<script setup>

import {SearchIcon} from "lucide-vue-next";
import {ref} from "vue";
const searchText = ref('')
const search = (link) => {
  if (link === ""){
    return null
  }
  else {
    event.preventDefault()
    window.location.href = 'https://www.google.com/search?q=' + link
    searchText.value = ''
  }
}

</script>

<template>
  <div class="Main">
    <form class="SearchForm select-none" @submit="search(searchText)">
      <input class="Search select-none " placeholder="Поиск..." v-model="searchText" spellcheck="false" autofocus>
      <button class="IconButton" @click="search(searchText)">
        <SearchIcon class="p-[3px]"/>
      </button>
    </form>
  </div>
</template>

<style scoped>
@media (max-width: 1024px) {
  .Main {
    width: 90%;
  }
}

@media (min-width: 1024px) {
  .Main {
    width: 50%;
  }
}

.body {
  background: black;
}

.SearchForm {
  display: flex;
  flex-direction: inherit;
  position: relative;
}
.Search {
  color: #ececec;
  font-size: 16px;
  font-family: Inter,sans-serif;
  word-wrap: break-word;
  border: 2px solid rgba(255, 255, 255, 0.01);
  outline: none;
  align-self: stretch;
  padding: 12px 15px 12px 20px;
  background: rgba(255, 255, 255, 0.10);
  border-radius: 4px;
  border-bottom: 2px #9C9C9C solid;
  backdrop-filter: blur(8px);
  justify-content: space-between;
  align-items: center;
  display: inline-flex;
  width: 100%;
  height: 48px;
  font-weight: normal;
}
.Search:hover {
  background: rgba(255, 255, 255, 0.08);
}
input::placeholder {
  color: rgba(255, 255, 255, 0.6);
  font-family: Inter,sans-serif;
  font-weight: normal;
}
.IconButton:hover {
  background: rgba(156, 156, 156, 0.1);
}
.IconButton:active {
  background: rgba(156, 156, 156, 0.05);
}
input:focus {
  border-radius: 4px;
  border-bottom: 2px solid #61CBFC;
  background: rgba(255, 255, 255, 0.05);
  backdrop-filter: blur(4px);
}
.IconButton {
  padding: 12px;
  justify-content: flex-start;
  align-items: center;
  display: flex;
  position: absolute;
  right: 8px;
  top: 4px;
  bottom: 6px;
  border: none;
  background-color: transparent;
  height: inherit;
  border-radius: 4px;
  cursor: pointer;
}

</style>