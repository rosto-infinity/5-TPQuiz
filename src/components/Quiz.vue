<template>
  <div class="container">
   <h1 style="font-size:2rem">{{ quizData.title}}</h1> 
   <Progress
    :value="step"
    :max="quizData.questions.length -1"
    class="mt"
    />

    <Question :question="question" v-if="question"/>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue';
import Progress from './Progress.vue';
import Question from './Question.vue';

const props =defineProps({
  quizData: Object
});
const step =ref(0);
const answers = ref(props.quizData.questions[step.value].correct_answer)

const question =computed(()=> props.quizData.questions[step.value])
</script>

<style  scoped>
  .mt{
    margin-top:2rem;
  }
</style>