<template>
  <div class="container">
    <h1>My Timetable App</h1>

    <!-- Days -->
    <div class="days">
      <button 
        v-for="day in days" 
        :key="day" 
        @click="selectDay(day)"
      >
        {{ day }}
      </button>
    </div>

    <!-- Subjects -->
    <div v-if="selectedDay" class="subjects">
      <h2>{{ selectedDay }}</h2>
      <ul>
        <li v-for="subject in timetable[selectedDay]" :key="subject">
          {{ subject }}
        </li>
      </ul>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue"

const days = ["Monday", "Tuesday", "Wednesday", "Thursday", "Friday"]

const selectedDay = ref(null)

const timetable = {
  Monday: ["UI/UX", "javascript", "free", "Math", "graphic design"],
  Tuesday: ["javascript", "javascript practice", "computer literacy", "version control"],
  Wednesday: ["version control", "game in vue", "free", "math"],
  Thursday: ["UI/UX", "javascript", "javascript practice", "physics", "javascript practice", "javascript practice"],
  Friday: ["game in vue", "french", "Sports and free"]
}

function selectDay(day) {
  selectedDay.value = day
}
</script>

<style>
.container {
  text-align: center;
  font-family: Arial;
  margin-top: 20px;
}

.days button {
  margin: 5px;
  padding: 10px;
  cursor: pointer;
}

.subjects {
  margin-top: 20px;
}
</style>
