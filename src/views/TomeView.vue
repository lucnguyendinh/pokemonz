<template>
    <Home v-if="currently === 'home'" @onStart="onHandleStart($event)" />
    <Play v-if="currently === 'play'" @win="goToWin" @lose="goToLose" :level="level" />
    <Result v-if="currently === 'result'" @again="goToHome" :isWin="isWin" />
</template>

<script setup>
import Home from '../components/Home.vue';
import Play from '../components/Play.vue';
import Result from '../components/Result.vue';

import { ref } from 'vue';

const currently = ref('home');
const isWin = ref(false);
const level = ref(0);
const onHandleStart = (config) => {
    level.value = config.totalBlock;
    currently.value = 'play';
};

const goToWin = () => {
    isWin.value = true;
    currently.value = 'result';
};

const goToLose = () => {
    currently.value = 'result';
};

const goToHome = () => {
    currently.value = 'home';
};
</script>

<style scoped module></style>
