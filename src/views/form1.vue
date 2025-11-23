<template>
  <h2>Please respond this small survey.</h2>
  <form @submit.prevent="save">
    <div>
      <label for="poolName">What's the name of the pool?</label>
      <input type="text" id="poolName" v-model="poolName"  />
    </div>
    <div>
      <label>Floor cleanliness:</label>
      <input type="range" min="1" max="5" v-model="floor" />
    </div>
    <div>
      <label>Crowdedness:</label>
      <select v-model="crowded">
        <option>0–2 people</option>
        <option>3–5</option>
        <option>6+</option>
      </select>
    </div>
    <div>
      <label>Showers working:</label>
      <input type="checkbox" v-model="showers" checked />
    </div>
    <div>
      <button>Submit</button>
    </div>
  </form>
</template>

<script setup>
import { ref } from 'vue';
import surveyData from '@/data/survey-questions.json';

const surveyQuestions = ref(surveyData);
const floor = ref(null);
const crowded = ref(null);
const showers = ref(null);
const poolName = ref(null);

function save() {
  // Clear previous responses
  localStorage.removeItem('responses');

  // Create the new entry
  const entry = {
    poolName: poolName.value,
    floor: floor.value,
    crowded: crowded.value,
    showers: showers.value,
  };

  // Store as a new array
  localStorage.setItem('responses', JSON.stringify([entry]));
  alert('Saved!');
}
</script>
