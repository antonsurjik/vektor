<template>
  <article class="quiz">
    <h1>Простой тест</h1>

    <article v-for="(question, index) in questions" class="question">
      <p>{{ index + 1 }}. {{ question.text }}</p>
      <article class="options">
        <label v-for="(option, optionIndex) in question.options">
          <input
            type="radio"
            :name="'question-' + index"
            :value="optionIndex"
            v-model="userAnswers[index]"
          />
          {{ option }}
        </label>
      </article>
    </article>

    <button @click="check_answers" :disabled="!isComplete">Завершить тест</button>

    <article v-if="showResult" class="result">
      <p>Вы ответили правильно на {{ correctAnswersCount }} из {{ questions.length }} вопросов!</p>
    </article>
  </article>
</template>

<script setup>
import { ref, computed } from "vue";

let questions = ref([
  {
    text: "Какой цвет не является основным?",
    options: ["Красный", "Желтый", "Зеленый", "Синий"],
    correctAnswer: 2,
  },
  {
    text: "Сколько планет в Солнечной системе?",
    options: ["7", "8", "9", "10"],
    correctAnswer: 1,
  },
  {
    text: "Какой язык используется для создания веб-приложений?",
    options: ["Python", "JavaScript", "C++", "Java"],
    correctAnswer: 1,
  },
]);

let userAnswers = ref(Array(questions.value.length));
let isComplete = computed(() => userAnswers.value.every((answer) => answer !== null));
let showResult = ref(false);
let correctAnswersCount = ref(0);

function check_answers() {
  correctAnswersCount.value = userAnswers.value.reduce((count, answer, index) => {
    return count + (answer === questions.value[index].correctAnswer ? 1 : 0);
  }, 0);

  showResult.value = true;
}
</script>

<style>
.quiz {
  font-family: Arial, sans-serif;
  padding: 20px;
  max-width: 600px;
  margin: 0 auto;
  text-align: left;
}

.question {
  margin-bottom: 20px;
}

.options {
  margin-top: 10px;
}

.options label {
  display: block;
  margin-bottom: 5px;
}

button {
  display: block;
  margin: 20px 0;
  padding: 10px 20px;
  font-size: 16px;
  background-color: #007bff;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.3s;
}

button:disabled {
  background-color: #cccccc;
  cursor: not-allowed;
}

button:hover:not(:disabled) {
  background-color: #0056b3;
}

.result {
  font-size: 18px;
  font-weight: bold;
  margin-top: 20px;
}
</style>