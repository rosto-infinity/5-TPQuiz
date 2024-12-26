<template>
  <div class="question">
    <h3>{{ question.question }}</h3>
    <ul>
      <li v-for="(choice, index) in question.choices" :key="choice">
        <label :for="`answer${index}`">
          <input
          v-model="answer"
           :id="`answer${index}`"
           :value="choice"
            type="radio" name="answer" />
          {{ choice }}
        </label>
      </li>
    </ul>


    
    <button 
    :disabled="!hasAnswer"
    @click="emits('answer', answer)">Question suivante </button>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'
const props =defineProps({
  question: Object,
});

const emits =defineEmits(['answer']);
const answer =ref(null);

const hasAnswer = computed(()=> answer.value !== null)
</script>

<style scoped>
.question {
  padding-top: 2rem;
}
.question button{
  margin-left:auto;
  display:block;
}
</style>