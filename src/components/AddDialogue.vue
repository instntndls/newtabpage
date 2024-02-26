<script setup>

import {
  AlertDialog,
  AlertDialogAction,
  AlertDialogCancel,
  AlertDialogContent,
  AlertDialogDescription,
  AlertDialogFooter,
  AlertDialogHeader,
  AlertDialogTitle,
  AlertDialogTrigger,
} from '@/components/ui/alert-dialog'
import {PlusSmallIcon} from "@heroicons/vue/24/outline/index.js";
import FavoriteButton from "@/components/FavoriteButton.vue";
import {Input} from "@/components/ui/input/index.js";
import {ref} from "vue";

const emit = defineEmits(['add'])

const link = ref('')

const addlink = () => {
  emit('add', link.value)
  link.value = ''
}
</script>

<template>
  <AlertDialog>
    <AlertDialogTrigger>
      <favorite-button><PlusSmallIcon class="size-7"/></favorite-button>
    </AlertDialogTrigger>
    <AlertDialogContent class="max-w-96 bg-white bg-opacity-[0.08] rounded-md backdrop-blur-xl border-0">
      <AlertDialogHeader>
        <AlertDialogTitle class="text-center">Добавьте новую закладку</AlertDialogTitle>
        <AlertDialogDescription class="pb-4 text-center">
          Введите ссылку на сайт который вы хотите добавить в закладки
        </AlertDialogDescription>
        <Input spellcheck="false" class="bg-transparent backdrop-blur-xl border-opacity-10" v-model="link" autofocus/>
      </AlertDialogHeader>
      <AlertDialogFooter>
        <div class="flex flex-row w-full items-center justify-end pt-2">
          <div>
            <AlertDialogAction :disabled="link === ''" class="mr-4 bg-white text-black hover:bg-black hover:text-white" @click="addlink">Сохранить</AlertDialogAction>
            <AlertDialogCancel class="bg-black text-white hover:bg-white hover:text-black ">Отмена</AlertDialogCancel>
          </div>
        </div>
      </AlertDialogFooter>
    </AlertDialogContent>
  </AlertDialog>
</template>

<style scoped>

</style>