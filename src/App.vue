<script setup>
import { reactive, ref } from "vue";
import Question from "./components/Question.vue";
import Result from "./components/Result.vue";

let questionAnswared = ref(0);
let totalCorrect = ref(0);
let questions = reactive([
  {
    q: "What is 2+2 ?",
    answer: [
      {
        text: "4",
        is_correct: true,
      },
      {
        text: "3",
        is_correct: false,
      },
      {
        text: "22",
        is_correct: false,
      },
      {
        text: "আমি জানিনা",
        is_correct: false,
      },
    ],
  },
  {
    q: "What reminder of 22%5 ?",
    answer: [
      {
        text: "1",
        is_correct: false,
      },
      {
        text: "2",
        is_correct: true,
      },
      {
        text: "5",
        is_correct: false,
      },
      {
        text: "ছকিনা জানে",
        is_correct: false,
      },
    ],
  },
  {
    q: "What is the capital of Bangladesh ?",
    answer: [
      {
        text: "Dhaka",
        is_correct: true,
      },
      {
        text: "Kolkata",
        is_correct: false,
      },
      {
        text: "22",
        is_correct: false,
      },
      {
        text: "আমি জানিনা",
        is_correct: false,
      },
    ],
  },
  {
    q: "Why The rajshahi Famourse for ?",
    answer: [
      {
        text: "Orange",
        is_correct: false,
      },
      {
        text: "Guava",
        is_correct: false,
      },
      {
        text: "Mango",
        is_correct: true,
      },
      {
        text: "Padma",
        is_correct: false,
      },
    ],
  },
])

let results = reactive([
  {
    min: 0,
    max: 2,
    title: "Try Again",
    des: "Do a title more studying and you may secceed!",
  },
  {
    min: 3,
    max: 3,
    title: "Wow, You are a genius!",
    des: "Studying has definitely paid off for you!",
  },
]);

// answer the question
let questionsAnswered = (isCorrect) => {
  if (isCorrect) {    
    totalCorrect.value++;
  }
    questionAnswared.value++;

    console.log(totalCorrect.value);
};

// reset
let reset = () => {
  questionAnswared.value = 0;
  totalCorrect.value = 0;
};
</script>

<template>
  <div class="container p-10">
    <transition name="fade" mode="out-in">
      <Question
        v-if="questionAnswared < questions.length"
        :questions="questions"
        :questionAnswared="questionAnswared"
        @question-Answared="questionsAnswered"
      />
      <Result v-else :results="results" :totalCorrect="totalCorrect" />
    </transition>

    <button
      type="button"
      class="mt-6 py-2 px-10 bg-blue-500 text-white font-semibold rounded-lg shadow-md hover:bg-blue-700 focus:outline-none focus:ring-2 focus:ring-blue-400 focus:ring-opacity-75"
      @click.prevent="reset"
      v-if="questionAnswared === questions.length"
    >
      Reset
    </button>
  </div>

</template>

<style scoped></style>
