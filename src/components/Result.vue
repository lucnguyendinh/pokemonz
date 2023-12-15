<template>
    <div class="wrapper__result">
        <h1 v-if="isWin">✨ Congratulations ✨</h1>
        <h1 v-else>✨ Try your best next time ✨</h1>
        <button class="btn__result" @click="handleAgain">Start again</button>
    </div>
</template>

<script setup>
// Props
const props = defineProps({
    isWin: {
        type: Boolean,
        required: true
    }
});
const { isWin } = props;
const emit = defineEmits(['again']);

const handleAgain = () => {
    emit('again');
};
</script>

<style scoped>
.wrapper__result {
    background-color: rgb(34, 36, 38);
    width: 100%;
    height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
}

.btn__result {
    width: 120px;
    height: 70px;
    border: 1px solid #fff;
    background-color: transparent;
    color: #fff;
    cursor: pointer;
    border-radius: 8px;
    font-size: 20px;
    margin-top: 100px;
}

.btn__result:hover {
    background-color: #fff;
    color: #000;
    transition: background 0.3s ease-in-out;
}
</style>
