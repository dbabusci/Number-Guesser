<script setup>
    import { ref } from 'vue';

    defineProps({
        title: String,
    })

    const guessCount = ref(0);
    const userNumber = ref(0);
    const randomNumber = ref(Math.floor(Math.random() * (101 - 1) + 1));
    const gameOver = ref(false);

    function assignUserNumber(input) {
        userNumber.value = Number(input);
        check();
        disabled();
    }

    function check() {
        ++guessCount.value;
        gameOver.value = userNumber.value == randomNumber.value;
    }

    function displayWinLoss(){
        if(gameOver.value == true){return "You got it!";}
        else{return "Keep guessing...";}
    }
    function disabled() {
        if(gameOver.value == true){return true;}
        else{return false;}
    }
</script>

<template>
    <h1>{{ title }}</h1>
    <button @click="assignUserNumber(number)" :disabled="gameOver">
        Guess
    </button>
    <input v-model="number" type="number" value="-1">
    <p>{{ displayWinLoss() }}</p>
    <p>Your guess count is: {{ guessCount }}</p>
</template>