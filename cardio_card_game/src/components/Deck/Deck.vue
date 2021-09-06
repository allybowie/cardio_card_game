<template>
    <div>
        <card />
    </div>
</template>

<script>
import Card from "../Card/Card.vue";
import cardValues from "../../data/cards.json";

export default {
    data() {
        return {
            cardValues,
            defaultExercises: [
                "Burpee",
                "Pushup",
                "Leg Raise",
                "Squat"
            ],
            exerciseOne: '',
            exerciseTwo: '',
            exerciseThree: '',
            exerciseFour: '',
            activeCard: null,
            finalDeck: []
        }
    },
    components: {
        Card
    },
    props: {
        customExercises: {
            type: Array,
            default: () => []
        } 
    },
    mounted() {
        this.finalDeck = this.shuffleDeck();
    },
    methods: {
        shuffleDeck() {
           if(!this.customExercises.length) {
                let deck = this.defaultExercises.reduce((deckArray, exercise) => {
                    
                    let exerciseValues = cardValues.cardValues.map(value => {
                        return {
                            value: value,
                            exercise: exercise
                        }
                    })
                    deckArray.push(exerciseValues);
                    return deckArray;
                }, [])
                
                return deck.flat()
            } 
        }
    },
    computed: {
        
    }
}
</script>

<style>

</style>