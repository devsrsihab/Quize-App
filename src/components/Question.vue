<script setup>
import { defineProps, defineEmits } from "vue";
defineProps(["questions", "questionAnswared"]);
const emit = defineEmits(["question-Answared"]);
const selectedAnswer = (is_correct) => {
  emit("question-Answared",is_correct);
};
</script>

<template>
  <div class="questions-ctr">
    <div class="progress">
      <div
        class="bar"
        :style="{ width: `${(questionAnswared / questions.length) * 100}%` }"
      >
        <div class="status">
          {{ questionAnswared }} out of {{ questions.length }}
        </div>
      </div>
      <transition-group name="fade">
        <div
          class="single-question"
          v-for="(question, index) in questions"
          :key="index"
          v-show="questionAnswared == index"
        >
          <div class="question">
            {{ question.q }}
          </div>
          <div class="answers">
            <div
              class="answer"
              v-for="answer in question.answer"
              :key="answer.text"
              @click.prevent="selectedAnswer(answer.is_correct)"
            >
              {{ answer.text }}
            </div>
          </div>
        </div>
      </transition-group>
    </div>
  </div>
</template>
