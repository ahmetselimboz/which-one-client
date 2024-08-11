<template>
    <div class="w-full p-4 bg-violet-700 flex items-center justify-center  text-white text-lg popping-regular tracking-wider select-none">
        ASB &copy {{ date }}
    </div>
</template>

<script setup>
import { ref } from 'vue';

const date = ref(new Date().getFullYear() )
</script>