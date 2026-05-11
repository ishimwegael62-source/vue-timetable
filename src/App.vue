<template>
  <div class="container">
    <h1>My Weekly Timetable</h1>

    <div class="day-buttons">
      <button
        v-for="(row, day) in schedule"
        :key="day"
        :class="{ active: selectedDay === day }"
        @click="selectDay(day)"
      >
        {{ day }}
      </button>
    </div>

    <div class="day-view" v-if="selectedDay">
      <div class="day-header">
        <div>
          <p class="subheading">Timetable for</p>
          <h2>{{ selectedDay }}</h2>
        </div>
        <button class="reset-button" @click="selectedDay = null">Show all days</button>
      </div>

      <div class="timeline">
        <div class="period-card period-label">
          <div class="period-number">Period</div>
          <div class="period-name">Subject</div>
        </div>

        <div
          v-for="(subject, index) in schedule[selectedDay]"
          :key="index"
          class="period-card"
          :class="subjectClass(subject)"
        >
          <div class="period-number">{{ periods[index] }}</div>
          <div class="period-name">
            <span v-if="subject">{{ subject }}</span>
            <span v-else class="empty-slot">Free</span>
          </div>
        </div>
      </div>

      <div class="legend">
        <div><span class="legend-box break"></span> Break</div>
        <div><span class="legend-box lunch"></span> Lunch</div>
      </div>
    </div>

    <div class="empty-state" v-else>
      Click any day above to display the horizontal timetable.
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue"

const periods = ["1", "2", "3", "Break", "4", "5", "6", "Lunch", "7", "Break", "8", "9"]

const schedule = {
  Monday: ["UI/UX", "", "", "Break", "DJF", "", "", "Lunch", "Math", "Break", "", "GD"],
  Tuesday: ["DJF", "", "", "Break", "DJF prac", "DJF prac", "DJF prac", "Lunch", "CL", "Break", "VC Prac", ""],
  Wednesday: ["VC", "", "", "Break", "DGV", "", "", "Lunch", "", "Break", "Math", ""],
  Thursday: ["UI/UX", "", "", "Break", "DJF", "DJF prac", "", "Lunch", "PHY", "Break", "DJF prac", ""],
  Friday: ["DGV", "", "", "Break", "FR", "", "", "Lunch", "", "Break", "", ""]
}

const selectedDay = ref(null)

function selectDay(day) {
  selectedDay.value = day
}

function subjectClass(subject) {
  if (subject === "Break") return "break"
  if (subject === "Lunch") return "lunch"
  return "subject"
}
</script>

<style>
.container {
  max-width: 1100px;
  margin: 20px auto;
  font-family: Inter, Arial, sans-serif;
  color: #05f539;
  padding: 0 18px 24px;
}

h1 {
  text-align: center;
  margin-bottom: 22px;
  font-size: clamp(2rem, 3vw, 2.6rem);
  letter-spacing: -0.03em;
}

.day-buttons {
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
  gap: 12px;
  margin-bottom: 28px;
}

.day-buttons button {
  background: #f1f5f9;
  border: 1px solid transparent;
  border-radius: 999px;
  padding: 12px 18px;
  cursor: pointer;
  font-weight: 600;
  color: #334155;
  transition: all 0.2s ease;
}

.day-buttons button.active,
.day-buttons button:hover {
  background: #2563eb;
  color: white;
  border-color: #1d4ed8;
}

.day-view {
  background: #ffffff;
  border: 1px solid #e2e8f0;
  border-radius: 24px;
  box-shadow: 0 20px 50px rgba(15, 23, 42, 0.08);
  padding: 24px;
}

.day-header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 16px;
  margin-bottom: 18px;
  flex-wrap: wrap;
}

.day-header h2 {
  margin: 0;
  font-size: 1.8rem;
}

.subheading {
  margin: 0 0 6px;
  color: #64748b;
  font-size: 0.95rem;
}

.reset-button {
  background: transparent;
  color: #2563eb;
  border: 1px solid #c7d2fe;
  border-radius: 999px;
  padding: 10px 16px;
  cursor: pointer;
  font-weight: 700;
}

.timeline {
  display: flex;
  overflow-x: auto;
  gap: 16px;
  padding-bottom: 12px;
  margin-bottom: 20px;
}

.timeline::-webkit-scrollbar {
  height: 8px;
}

.timeline::-webkit-scrollbar-thumb {
  background: #cbd5e1;
  border-radius: 999px;
}

.period-card {
  flex: 0 0 170px;
  min-width: 170px;
  border-radius: 22px;
  padding: 18px 16px;
  display: grid;
  gap: 12px;
  border: 1px solid #e2e8f0;
  background: #f8fafc;
  transition: transform 0.2s ease, box-shadow 0.2s ease;
}

.period-card:hover {
  transform: translateY(-4px);
  box-shadow: 0 16px 30px rgba(15, 23, 42, 0.08);
}

.period-label {
  background: #e2e8f0;
  color: #0f172a;
  text-align: left;
}

.period-number {
  font-size: 0.85rem;
  font-weight: 700;
  letter-spacing: 0.03em;
  text-transform: uppercase;
  color: #475569;
}

.period-name {
  font-size: 1.05rem;
  font-weight: 700;
  line-height: 1.4;
  min-height: 52px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.empty-slot {
  color: #64748b;
  font-weight: 500;
}

.subject {
  background: #eff6ff;
  border-color: #bfdbfe;
}

.break {
  background: #fef3c7;
  border-color: #fde68a;
}

.lunch {
  background: #d1fae5;
  border-color: #86efac;
}

.legend {
  display: flex;
  justify-content: center;
  gap: 24px;
  margin-top: 8px;
  font-size: 14px;
}

.empty-state {
  margin-top: 24px;
  color: #475569;
  font-size: 16px;
  text-align: center;
}

.legend-box {
  display: inline-block;
  width: 16px;
  height: 16px;
  margin-right: 8px;
  vertical-align: middle;
  border: 1px solid #94a3b8;
  border-radius: 4px;
}

.legend-box.break {
  background: #fde68a;
}

.legend-box.lunch {
  background: #a7f3d0;
}

@media (max-width: 740px) {
  .period-card {
    flex: 0 0 140px;
    min-width: 140px;
  }

  .day-header {
    flex-direction: column;
    align-items: flex-start;
  }
}
</style>
