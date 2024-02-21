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

    function disabled() {
        if(gameOver.value == true){return true;}
        else{return false;}
    }

    function highLow() {
        if(userNumber.value > randomNumber.value){
            return "You number is higher than the random number...";
        }
        else if(userNumber.value < randomNumber.value){
            return "Your number is lower than the random number...";
        }
        else{
            return "You got it";
        }
    }
</script>

<template>
    <h1>{{ title }}</h1>
    <button @click="assignUserNumber(number)" :disabled="gameOver">
        Guess
    </button>
    <input v-model="number" type="number" value="-1">
    <p>Your guess count is: {{ guessCount }}</p>
    <p>{{ highLow() }}</p>
</template>