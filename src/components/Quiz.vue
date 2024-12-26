<template>
  <div class="container">
   <h1 style="font-size:2rem">{{ quizData.title}}</h1> 
   <Progress
    :value="step"
    :max="quizData.questions.length -1"
    class="mt"
    />
    <Question :question="question" v-if="question" @answer="addAnswer"/>
    {{ answers}}
  </div>
</template>

<script setup>
import { ref, computed } from 'vue';
import Progress from './Progress.vue';
import Question from './Question.vue';

const props =defineProps({
  quizData: Object
});
const answers = ref(props.quizData.questions.map(() => null));
const step =ref(0);
const question =computed(()=> props.quizData.questions[step.value]);

const addAnswer =(answer) =>{
  answers.value[step.value] = answer;
  
  // if (step.value < props.quizData.questions.length - 1) {
  //   step.value++;
  // } else {
  //   // Logique pour terminer le quiz
  //   console.log("Quiz terminé");
  // }
}
</script>

<style  scoped>
  .mt{
    margin-top:2rem;
  }
</style>