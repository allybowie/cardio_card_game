<template>
    <div>
        <btn text="Create New Workout" v-on:click.native="createNewWorkout"/>
        <btn v-if="!deckEmpty" text="Draw Card" v-on:click.native="drawCard"/>
        <div v-else>
            <btn text="Shuffle Deck" v-on:click.native="shuffleDeck"/>
            <h3>Workout Complete</h3>
        </div>
        <card v-if="activeCard && !deckEmpty" :cardInfo="activeCard"/>
    </div>
</template>

<script>
import Card from "../Card/Card.vue";
import Button from "../Button/Button.vue";
import cardValues from "../../data/cards.json";

export default {
    data() {
        return {
            cardValues,
            exerciseOne: '',
            exerciseTwo: '',
            exerciseThree: '',
            exerciseFour: '',
            activeCard: {},
            deck: [],
            deckEmpty: false
        }
    },
    components: {
        Card,
        btn: Button
    },
    props: {
        exercises: {
            type: Array,
            required: true
        } 
    },
    mounted() {
        this.shuffleDeck();
    },
    methods: {
        createNewWorkout() {
            this.$emit("createNewWorkout", true);
        },
        shuffleDeck() {
            let deck = this.exercises.reduce((deckArray, exercise) => {
                console.log("Shuffling cards: ",exercise )
                    
                let exerciseValues = cardValues.cardValues.map(card => {
                    const cardInfo = {
                        value: card.value,
                        exercise: exercise.exercise
                    }

                    if(card.face) cardInfo.face = card.face
                    return cardInfo
                })
                deckArray.push(exerciseValues);
                return deckArray;
            }, [])
                
            this.deck = deck.flat();
            this.deckEmpty = false;
            this.activeCard = {};
        },
        drawCard() {
            if(!this.deck.length) {
                this.deckEmpty = true;
                return;
            }
            let index = Math.floor(Math.random() * this.deck.length);
            this.activeCard = this.deck.splice(index, 1)[0]; 
        }
    }
}
</script>

<style>

</style>