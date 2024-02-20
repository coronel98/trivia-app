<script setup>
import { onMounted, ref } from 'vue'
import BaseTitle from '@/components/BaseTitle.vue';
import useAPI from '@/composables/useAPI'

const { categories, getCategories } = useAPI()

onMounted(async () => {
  await getCategories()
})


</script>

<template>
  <h1 class="text-center" >TRIVIA APPLICATION</h1>
  <div class="grid flex-grow grid-cols-4 gap-12 m-20">
      {{  category.name }}
  </div>  

 
</template>