<script setup lang="ts">
import { ref, computed, onUnmounted, onMounted } from 'vue'

const count = ref(0)
const score = ref(0)
const userAnswer = ref('')
const QuestionsAnswersArr = ref([
  { q: "1+3", a: "4" },
  { q: "3+3", a: "6" },
  { q: "6+3", a: "9" },
])
let intervalId = null

onMounted(() => {
  intervalId = setInterval(check, 4000)
})

const questions = computed(() => {
  return QuestionsAnswersArr.value[count.value].q
})

const rightAnswer = computed(() => {
  return QuestionsAnswersArr.value[count.value].a
})

const areWeDone = computed(() => {
  return count.value >= QuestionsAnswersArr.value.length;
})

const check = () => {
  console.log('checked!');

  if (rightAnswer.value === userAnswer.value) {
    score.value++
  }
  count.value++
  userAnswer.value = ''

}

onUnmounted(() => {
  if (areWeDone.value) {
    clearInterval(intervalId)
  }
})

</script>

<template>

  <div>
    {{ areWeDone ? `Your Score: ${score}` : 'Next Question' }}
  </div>

  <div class="card" v-if="!areWeDone">
    <p>{{ questions }}</p>
    <input type="text" v-model="userAnswer">
  </div>
</template>

<style scoped>
.read-the-docs {
  color: #888;
}
</style>
