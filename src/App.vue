<script setup lang="js">
import Quiz from './components/Quiz.vue'
import { onMounted, ref } from 'vue';

const quiz = ref(null);
const state = ref('loading')

onMounted(async () => {
  try {
    state.value = 'idle'
    const response = await fetch('quiz.json')
    const data = await response.json()
    quiz.value = data
  }
  catch (error) {
    console.log('Error' + error)
    state.value = 'error'
  }
  finally { 
    state.value = false
  }
})
</script>

<template>
  <div class="container">
    <div v-if="state === 'error'">
      <p>Impossible de charger le quiz</p>
    </div>
    <div :aria-busy="state === 'loading'">
      <Quiz :quiz="quiz" v-if="quiz" />
    </div>  
  </div>
</template>

<style>
.conmtainer {
  margin: 20px auto;
}
</style>