<template>
    <dialog
          class="modal mx-auto fixed inset-0 flex items-center justify-center bg-black bg-opacity-50 z-50 w-full h-full"
        >
        <div class="md:w-[40%] w-[95%] bg-white rounded-lg p-5 relative">
                <button @click="$emit('close')" class="rounded-full px-2 py-1 btn-ghost absolute right-3 z-20 top-3 bg-slate-300 hover:bg-slate-400">✕</button>
            <div v-if="singleUser">
                <h1 class="font-bold text-2xl capitalize">{{ singleUser.title }}</h1>
                <div class="flex gap-5 items-center text-xs">
                    <span class="text-green-600 bg-green-200 border border-green-600 rounded-full px-2 py-1">ID: {{ singleUser.id }}</span>
                    <span class="text-rose-800 border border-rose-800 bg-rose-200 px-2 py-1 rounded-full">User ID: {{ singleUser.userId }}</span>
                </div>
                <p class="mt-4">{{ singleUser.body }}</p>
            </div>
        </div>
    </dialog>
</template>
    
<script setup>
import { ref, defineEmits } from 'vue';
    
const props = defineProps(['singleUser']);
const emit = defineEmits(['close']);
</script>