<script setup>
import { defineProps, computed } from "vue";

const userName = 'sohan'
const userEmail = ''
const props = defineProps(["results", "totalCorrect"]);

// the result show ofr try again or Good Done
let resutlIndex = computed(() => {
  let index = 0;

  props.results.forEach((e, key) => {
    if (e.min <= props.totalCorrect && e.max >= props.totalCorrect) {
      index = key;
    }
  });

  return index;
});
</script>

<template>
  <div class="result">
    <div :class="(index ? 'bg-red-500' : 'bg-green-500')" class="title">
      {{ results[resutlIndex].title }}
    </div>
    <div class="desc">{{ results[resutlIndex].des }}</div>
  </div>
</template>
