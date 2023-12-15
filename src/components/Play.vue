<template>
    <div class="wrapper">
        <h1>POKE MEMORI</h1>
        <p v-if="level !== 0">Time Left: {{ timeLeft }}</p>
        <div class="container">
            <Card
                v-for="(card, index) in cards"
                :key="index"
                :img="`images/${card}.png`"
                :card="card"
                :index="index"
                @onFlip="handleFlipCard($event)"
                ref="itemRefs"
            />
        </div>
        <p>This game owned by LucNguyen in Vue 3 course for begginers</p>
    </div>
</template>
<script setup>
import Card from './Card.vue';
import { ref, computed, onMounted } from 'vue';

const emit = defineEmits(['win', 'lose']);

// Props
const props = defineProps({
    level: {
        type: Number,
        required: true
    }
});
const { level } = props;

const timeLeft = ref(150 * level);

onMounted(() => {
    if (level !== 0) {
        setInterval(() => {
            if (timeLeft.value === 0) {
                emit('lose');
            }
            timeLeft.value--;
        }, 1000);
    }
});

const listCard = ref([]);
for (let i = 1; i <= 25; i++) {
    listCard.value.push(i);
    listCard.value.push(i);
}

const rules = ref([]);
const count = ref(0);
const itemRefs = ref([]);

const cards = computed(() => {
    return listCard.value.slice().sort(soSanhNgauNhien);
});

const soSanhNgauNhien = () => {
    return Math.random() - 0.5;
};

const handleFlipCard = ({ card, index }) => {
    if (rules.value.length === 2) return;

    itemRefs.value[index].onFlip();

    rules.value.push({ card, index });

    if (rules.value.length === 2) {
        if (rules.value[0].index === rules.value[1].index) {
            rules.value = [];
        } else if (rules.value[0].card === rules.value[1].card) {
            if (count.value === 24) {
                setTimeout(() => {
                    emit('win');
                }, 920);
            }
            itemRefs.value[rules.value[0].index].onDisable();
            itemRefs.value[rules.value[1].index].onDisable();
            count.value++;

            rules.value = [];
        } else {
            setTimeout(() => {
                itemRefs.value[rules.value[0].index].onFlipBack();
                itemRefs.value[rules.value[1].index].onFlipBack();

                rules.value = [];
            }, 800);
        }
    }
};
</script>

<style scoped>
.wrapper {
    background-image: url('../assets/background/playscreen.png');
    object-fit: cover;
    background-size: cover;
    background-position: center center;
    width: 100%;
    height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
}
.container {
    display: flex;
    flex-wrap: wrap;
    width: 1100px;
}
</style>
