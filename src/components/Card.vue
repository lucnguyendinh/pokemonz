<template>
    <div class="card" :class="{ disable: isDisabled }" @click="handleFlipCard">
        <div class="front" v-show="isFlipped">
            <img :src="'/src/assets/' + img" alt="" />
        </div>
        <div class="back" v-show="!isFlipped">
            <img src="../assets/images/icon_back.png" alt="" />
        </div>
    </div>
</template>

<script setup>
import { ref } from 'vue';

const emit = defineEmits(['onFlip']);

const props = defineProps({
    card: {
        type: Number
    },
    index: {
        type: Number
    },
    img: {
        type: String,
        required: true
    }
});

const { card, index, img } = props;

const isFlipped = ref(false);
const isDisabled = ref(false);

const handleFlipCard = () => {
    if (isDisabled.value) return;

    emit('onFlip', { card, index });
};

const onFlip = () => {
    isFlipped.value = !isFlipped.value;
};

const onFlipBack = () => {
    isFlipped.value = false;
};

const onDisable = () => {
    isDisabled.value = true;
};

defineExpose({
    onFlipBack,
    onDisable,
    onFlip
});
</script>

<style scoped>
.card {
    width: 90px;
    height: 120px;
    border-radius: 4px;
    position: relative;
    cursor: pointer;
    margin: 8px 8px;
    background-color: #dedede;
}

.front,
.back {
    position: absolute;
    width: 100%;
    height: 100%;
    border-radius: 4px;
}

.front img {
    background-position: center center;
    background-repeat: no-repeat;
    background-size: contain;
    height: 100%;
    width: 100%;
}

.back img {
    background-position: center center;
    background-repeat: no-repeat;
    background-size: contain;
    height: 100%;
    width: 100%;
}

.disable {
    cursor: default;
    background-color: rgb(162, 165, 168);
}
</style>
