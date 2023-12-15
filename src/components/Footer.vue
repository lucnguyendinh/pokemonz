<template>
    <div>
        <h2>Xin chào {{ name }}, bạn đã {{ age }} tuổi</h2>
        <h1>{{ formattedHeight }}</h1>
        <button @click="addHight">Thêm 1 cm</button>
        <button @click="emitEvent">Send emit</button>
    </div>
</template>

<script setup>
//import
import { defineProps, ref, computed } from 'vue';

// Biến
const height = ref(183);

// Props
const props = defineProps({
    name: {
        type: String,
        required: true
    },
    age: {
        type: String,
        required: true
    }
});
const { name, age } = props;

// Computed
const formattedHeight = computed(() => {
    return `Bạn cao ${height.value} cm`;
});

// Phương thức
const addHight = () => {
    height.value += 1;
};

//emit event len component cha
const emit = defineEmits(['emit-event']);

const emitEvent = () => {
    emit('emit-event', 1);
};
</script>

<style scoped module>
.hello {
    font-size: 50px;
}
</style>
