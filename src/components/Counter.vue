<template>
    <div>
        <button @click="incrementCount" class="mt-4 bg-green-500 text-white py-2 px-3 rounded-md">Increment Count</button>
        <p class="font-bold">Count: {{ count }}</p>
    </div>
</template>

<script setup>
import { ref } from 'vue';

const count = ref(0);

const incrementCount = () => {
      count.value = count.value >= 100 ? 0 : count.value + 1;
    };
</script>