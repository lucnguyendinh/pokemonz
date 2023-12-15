<template>
    <div :class="[$style.wrapper]">
        <h1>POKE MEMORIES</h1>
        <p>Select mode to start game</p>
        <div :class="[$style.action]">
            <div :class="[$style.item]" @click="onStart(0)">
                <h3>Easy</h3>
            </div>
            <div :class="[$style.item]" @click="onStart(2)">
                <h3>Normal</h3>
            </div>
            <div :class="[$style.item]" @click="onStart(1)">
                <h3>Hard</h3>
            </div>
        </div>
    </div>
</template>

<script setup>
const emit = defineEmits(['onStart']);

//methods
const onStart = (totalBlock) => {
    emit('onStart', { totalBlock });
};
</script>

<style scoped module>
.wrapper {
    width: 100%;
    height: 100vh;
    background-color: rgb(40, 43, 45);
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
}
.action {
    display: flex;
    margin: 100px;
}

.action .item {
    margin: 0 16px;
    padding: 4px;
    cursor: pointer;
    width: 100px;
    height: 100px;
    border: 1px solid #fff;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    border-radius: 8px;
}

.action .item:hover {
    background-color: #fff;
    color: #000;
    transition: background 0.3s ease-in-out;
}
</style>
