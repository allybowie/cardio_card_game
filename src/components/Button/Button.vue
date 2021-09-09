<template>
    <div class="buttonContainer">
        <p>{{ text }}</p>
    </div>
</template>

<script>
export default {
    props: {
        text: {
            type: String,
            default: 'Create Workout'
        }
    }
}
</script>

<style>
.buttonContainer {
    border: black 2px solid;
    border-radius: 4px;
    width: 100px
}
</style>