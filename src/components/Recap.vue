<template>
  <h1>Recap</h1>
  <p>Votre score est : {{ score }} /{{ quizData.questions.length}}</p>
  <p>{{ resultMessage }}</p>
</template>


<script setup>
import { computed} from 'vue';

  const props = defineProps({
    answers: {
      type: Array,
      required: true
    },
    quizData: {
      type: Object,
      required: true
    }
  });

  const score = computed(() => {
    return props.quizData.questions.reduce((acc, question, index) => {
      if (question.correct_answer === props.answers[index]) {
        return acc + 1;
      }
      return acc;
    }, 0);
  });

  const resultMessage = computed(() => {
    return score.value >= props.quizData.minimum_score
      ? props.quizData.success_message
      : props.quizData.failure_message;
  });
</script>