<script setup>

import draggable from 'vuedraggable'
import {inject, onMounted, ref} from "vue";
import FavoriteButton from "@/components/FavoriteButton.vue";
import AddDialogue from "@/components/AddDialogue.vue";
import {handler} from "tailwindcss-animate";

const myArray = ref([])
const trash = ref([])
const drag = ref(false)

const saveToLocalStorage = () => {
  localStorage.setItem('favorites', JSON.stringify(myArray.value))
}
const getFromLocalStorage = () => {
  myArray.value = JSON.parse(localStorage.getItem('favorites'))
}

const uuid = () => {
  let id = myArray.value.length + 1;
  while (myArray.value.some(element => element.id === id)) {
    id++;
  }
  return id;
}

const addToLocalStorage = (link) => {
  myArray.value.push({id: uuid(), name: link})
  saveToLocalStorage()
  getFromLocalStorage()
}

// const deleteFromLocalStorage = (id) => {
//   myArray.value = myArray.value.filter((item) => item.id !== id)
//   saveToLocalStorage()
//   getFromLocalStorage()
// }

const clearTrash = () => {
  trash.value = null
}

const openInNewTab = (link) => {
  window.open(link, '_blank')
}
const openInThisTab = (link) => {
  window.location.href = link
}

onMounted( () => {
  clearTrash()
  getFromLocalStorage()
  if (myArray.value === null) {
    myArray.value = []
  }
})

</script>

<template>
    <div class="Main h-min w-full z-10 flex justify-center gap-6">
    <draggable
        v-model="myArray"
        group="people"
        @start="drag=true; clearTrash()"
        @end="drag=false; saveToLocalStorage()"
        item-key="id"
        animation="200"
        class="flex flex-row gap-6"
    >
      <template #item="{ element }">
        <favorite-button @click="openInThisTab(element.name)" @mousedown.middle="openInNewTab(element.name)">
          <img class="select-none size-5" :src="'https://s2.googleusercontent.com/s2/favicons?domain_url=' + element.name" :alt="element.name">
        </favorite-button>
      </template>
      </draggable>
      <AddDialogue @add="addToLocalStorage" />
    </div>
    <transition>
      <div v-if="drag" class="flex justify-center items-center bg-red-500 bg-opacity-30 rounded-md h-24 w-full absolute z-10 bottom-0 right-0">
        <p class="text-white text-2xl absolute text-opacity-60">Удалить</p>
        <draggable
            v-model="trash"
            group="people"
            @start="drag=true"
            @end="drag=false"
            item-key="id"
            class="flex h-full items-center justify-center"
        >
          <template #item>
            <FavoriteButton/>
          </template>
        </draggable>
      </div>
    </transition>
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
.v-enter-active,
.v-leave-active {
  transition: opacity 0.1s ease;
}

.v-enter-from,
.v-leave-to {
  opacity: 0;
}
</style>