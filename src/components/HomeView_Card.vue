<template>
    <div class="w-[370px] bg-black rounded-md h-fit flex flex-col overflow-hidden">
        <div class="w-full h-3/4">
            <img :src="card.item.imageUrl" class="w-full h-[225px] object-cover" alt="">
        </div>
        <div class="w-full h-1/4 py-4 px-2 bg-slate-300">
            <div class="text-3xl font-bubblegum text-slate-800 px-1">{{ card.item.title }}</div>
            <div class="w-full flex flex-row items-center my-1">
                <div class="w-1/2 py-3 px-2 text-xs poppins-regular text-violet-800">
                    {{ card.item.description }}
                </div>
                <div class="w-1/2 flex items-center justify-center">
                    <router-link :to="`/quiz/${card.item._id}`" class="flex flex-row items-center gap-1 text-lg rounded-md poppins-medium text-white bg-indigo-500 hover:bg-indigo-600 transition-all cursor-pointer py-2 px-5">
                        <i class="pi pi-caret-right"></i>
                        Başla!
                    </router-link>
                </div>
            </div>
        </div>
    
    </div>
</template>

<script setup>
import { onMounted, ref } from 'vue';


const props = defineProps(["item"])

const card = ref(props.item)

onMounted(()=>{
    console.log(card.value.item.tite)
})
</script>