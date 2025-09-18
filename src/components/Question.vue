<script setup lang="js">
import { computed, onMounted, onUnmounted, ref, watch } from 'vue';
import Answer from './Answer.vue';

    const props = defineProps({
        question: {
            type: Object,
        }
    }); 

    const answer = ref(null)
    const emits = defineEmits(['answer'])
    const hasAnswer = computed(() => answer.value !== null)
</script>

<template>
    <div class="question">
        <h3>{{ question.question }}</h3>
        <ul>
            <li v-for="(choice, index) in question.choices" :key="choice">
                <label :for="`answer-${index}`">
                    <input type="radio" name="answer" :id="`answer-${index}`" v-model="answer" :value="choice">
                    {{ choice }}
                </label>
            </li>
        </ul>
        {{ answer }}
        <br>
        <button :disabled="!hasAnswer" @click="emits('answer', answer)">Question suivante</button>
    </div>
</template>

<style>
.question {
    padding-top: 2rem;
}
</style>