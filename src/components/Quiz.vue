<template>
  <div class="container">
   <h1 style="font-size:2rem">{{ quizData.title}}</h1> 
   
    <Progress
    :value="step"
    :max="quizData.questions.length -1"
    class="mt"
    />
    
    <span style="color:rgb(150,222,0);">{{ pourcentage }}%</span>
  
    <Question
      :key="question.question"
      :question="question" v-if="state==='question'" 
      @answer="addAnswer"/>
    <Recap v-if="state== 'recap'" :answers="answers" :quizData="quizData" />
    {{ answers}}
  </div>
</template>

<script setup>
import { computed, ref } from 'vue';
import Progress from './Progress.vue';
import Question from './Question.vue';
import Recap from './Recap.vue';

const props =defineProps({
  quizData: Object
});

const state =ref('question');
const answers = ref(props.quizData.questions.map(() => null));
const step =ref(0);
const question =computed(()=> props.quizData.questions[step.value]);

const addAnswer =(answer) =>{
  answers.value[step.value] = answer;
  if (step.value === props.quizData.questions.length - 1) {
    state.value = 'recap';
  } else {
    step.value++;
    
  }
}

const pourcentage = computed(() => {
  return Math.round((step.value / (props.quizData.questions.length - 1)) * 100);
});
</script>

<style  scoped>
  .mt{
    margin-top:2rem;
  }
  
</style>