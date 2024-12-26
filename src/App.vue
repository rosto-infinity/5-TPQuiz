<template>
  <div class="container" style="margin-top:2rem">
    <div v-if="state === 'erreur'" class="error">
    
        Impossible de charger le quiz
    
    </div>
    <div v-else-if="quizData">

      <!-- <pre>{{ quizData }}</pre> -->
     <Quiz :quizData="quizData" v-if="quizData"/>
    
    </div>
    <div v-else>Chargement..</div>
  </div>
</template>

<script setup>
import { onMounted, ref } from "vue";
import Quiz from "./components/Quiz.vue";

const quizData = ref(null);
const state = ref("loading");

onMounted(async () => {
  try {
    const response = await fetch("/quiz.json");
    if (!response.ok) {
      throw new Error("Erreur lors du chargement du quiz");
    }
    const data = await response.json();
    quizData.value = data;
    state.value = "idle";
  } catch (error) {
    console.error("Erreur:", error);
    state.value = "erreur";
  }
});
</script>