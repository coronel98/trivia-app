<script setup>
import { onMounted, ref } from 'vue';
import useAPI from '@/composables/useAPI';
import { useRoute } from 'vue-router';
import BaseTitle from '@/components/BaseTitle.vue';
const api = useAPI()
const question = ref(null)
const route = useRoute()
const answers = ref([])
onMounted(async () => {
  question.value = await api.getQuestion(route.params.id)

  answers.value.push({
    id: answers.value.length,
    correct: true,
    answer: question.value.correct_answer
  })

  question.value.incorrect_answers.map((wrong_answer) => {
    answers.value.push({
      id: answers.value.length,
      correct: false,
      answer: wrong_answer
    })

  })

  answers.value = shuffle(answers.value)
  // console.log(question.value)

})

</script>


<template>

<div v-if="question" class="flex h-full w-full flex-col items-center gap-8 p-10">
  <BaseTitle>{{  question.category }}</BaseTitle>
  

</div>
<div v-else class="">
  Loading...
</div>

</template>