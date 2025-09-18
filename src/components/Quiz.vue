<script lang="js" setup>
import Question from './Question.vue';
import Progress from './Progress.vue';
import { computed, ref } from 'vue';

const props = defineProps({
  quiz: {
    type: Object,
    required: true
  }
})
const step = ref(0)

const question = computed(() => {
  return props.quiz.questions[step.value]
})

const answers = ref(props.quiz.questions.map(() => null))
const addAnswer = (answer) => {
  answers.value[step.value] = answer
  if (step.value < props.quiz.questions.length - 1) {
    step.value++
  } else {
    console.log('Quiz terminé', answers.value)
  }
}
</script>

<template>
  <div class="quiz">
    <h1>{{ quiz.title }}</h1>  
    <Progress v-if="quiz" :value="step" :max="quiz.questions.length - 1" />
    <Question v-if="question" :question="question" />
  </div>
</template>