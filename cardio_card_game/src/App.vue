<template>
  <div id="app">
    <h1>Cardio Card Game</h1>
    <Deck />
    <input v-for="(exercise, index) in defaultExercises" :key="`input-exercise-${index}`" :v-model="`customExercise${index+1}`" :value="exercise.exercise" :placeholder="exercise.exercise"/>
  </div>
</template>

<script>
import Deck from "./components/Deck/Deck.vue";

export default {
  name: 'App',
  components: {
    Deck
  },
  data() {
    return {
      defaultExercises: [
        {
          suit: "clubs",
          exercise: "Burpee"
        },
        {
          suit: "hearts",
          exercise: "Pushup"
        },
        {
          suit: "diamonds",
          exercise: "Leg Raise"
        },
        {
          suit: "spades",
          exercise: "Squat"
        }
      ],
      customExercise1: '',
      customExercise2: '',
      customExercise3: '',
      customExercise4: ''
    }
  },
  mounted() {
    this.setDefaults();
  },
  methods: {
    setDefaults() {
      this.defaultExercises.forEach((exercise, index) => {
          this[`customExercise${index+1}`] = exercise.exercise;
      });
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
