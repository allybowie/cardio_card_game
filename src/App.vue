<template>
  <div id="app">
    <h1>Cardio Card Game</h1>
    <div v-if="!workoutInProgress">
      <h3>Create Your Workout</h3>
      <form v-on:keyup.enter="createWorkout">
        <input
          v-for="(exercise, index) in defaultExercises"
          :key="`input-exercise-${index}`"
          v-model="customExercises[index+1]"
          :placeholder="exercise.exercise"
          class="input"
          type="text"
          />
      <btn class="buttonContainer" v-on:click.native="createWorkout"/>
      </form>
    </div>
    <Deck class="deckContainer" v-else :exercises="finalExercises" v-on:createNewWorkout="returnToWorkout($event)"/>
  </div>
</template>

<script>
import Deck from "./components/Deck/Deck.vue";
import Button from "./components/Button/Button.vue";


export default {
  name: 'App',
  components: {
    Deck,
    btn: Button
  },
  data() {
    return {
      workoutInProgress: false,
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
      customExercises: {
        1: '',
        2: '',
        3: '',
        4: ''
      }
    }
  },
  mounted() {
    this.setDefaults();
  },
  computed: {
    finalExercises() {
      return this.defaultExercises.map((exercise, index) => {
        const finalExercise = exercise;
        
        if(this.customExercises[index+1]) finalExercise.exercise = this.customExercises[index+1].charAt(0).toUpperCase() + this.customExercises[index+1].slice(1);
        return finalExercise
      })
    }
  },
  methods: {
    returnToWorkout() {
      this.workoutInProgress = false;
    },
    setDefaults() {
      this.defaultExercises.forEach((exercise, index) => {
          this.customExercises[index+1] = exercise.exercise;
      });
    },
    createWorkout() {
      this.workoutInProgress = true;
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

.input {
  padding: 5px;
  margin: 0 10px 0 10px;
}

.deckContainer {
  margin: 0 auto;
  max-width: 200px;
}

@media(max-width: 1023px) {
  .input {
    margin: 0 10px 10px 10px
  }
}

.buttonContainer {
  margin: 30px auto;
  cursor: pointer;
}
</style>
