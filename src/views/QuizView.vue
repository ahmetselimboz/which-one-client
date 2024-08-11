<template>
  <Navbar />
  <div class="w-full h-full flex justify-center pb-10">
    <div class="lg:w-2/3 w-full flex flex-col">
      <div class="flex justify-center">
        <img :src="items.imageUrl" class="w-3/4 rounded-md" alt="" />
      </div>
      <div
        class="w-full px-4 text-violet-700 font-bold lg:text-5xl text-4xl my-10 font-bubblegum lg:text-left text-center"
      >
        {{ items.title }}
      </div>

      <div class="w-full flex flex-col items-center">
        <template v-for="(item, i) in items.questions">
          <div
            class="lg:w-full w-5/6 bg-slate-300/50 rounded-md px-4 py-6 my-4"
          >
            <div class="w-full poppins-regular text-lg">
              {{ i + 1 }}-) {{ item.title }}
            </div>
            <div class="w-full my-4 px-3">
              <div class="w-full" v-for="(answer, index) in item.options">
                <div
                  @click="selectOption(i, index, answer.weights)"
                  :class="[
                    selectedOption[i] === index
                      ? 'bg-green-400 text-gray-100'
                      : 'bg-slate-300 hover:bg-slate-400/50 text-gray-800',
                    ' transition-all px-2 py-3 my-2  text-lg cursor-pointer',
                  ]"
                >
                  <i
                    v-if="selectedOption[i] === index"
                    class="fa-regular fa-circle-dot mr-2"
                  ></i>
                  <i v-else class="fa-regular fa-circle mr-2"></i>
                  {{ answer.text }}
                </div>
              </div>
            </div>
          </div>
        </template>
      </div>
      <div class="w-full flex items-center justify-center my-4">
        <button
          v-if="selectedAnswer.length === 10"
          @click="getResult()"
          class="flex items-center gap-2 poppins-regular px-4 py-2 rounded-md bg-violet-700 hover:bg-violet-800 transition-all text-white text-lg cursor-pointer"
        >
        <i class="pi pi-caret-right"></i>
          Sonucu Gör
        </button>
        <button
          v-else
          class="flex items-center gap-2 poppins-regular px-4 py-2 rounded-md bg-violet-700/80 text-white text-lg pointer-events-none select-none"
          disabled
        >
        <i class="pi pi-caret-right"></i>
          Sonucu Gör
        </button>
      </div>
      <div v-if="show" class="my-5 px-4">
        <div class="font-bubblegum text-gray-800 text-5xl my-1">{{result}}</div>
        <div class="poppins-light text-gray-700 text-xl">{{items.results[result]}}</div>
      </div>
    </div>
  </div>
</template>

<script setup>
import Navbar from "@/components/Navbar.vue";
import axios from "axios";
import { onBeforeMount, reactive, ref } from "vue";
import { useRoute } from "vue-router";

const route = useRoute();

const items = ref({});
const show = ref(false);

const result = ref("");

const selectedOption = reactive({});
const selectedAnswer = reactive([]);

const selectOption = (questionIndex, answerIndex, answerWeight) => {
  selectedOption[questionIndex] = answerIndex;
  selectedAnswer[questionIndex] = answerWeight;
};

const getResult = () => {
  let totalScores = {};

  selectedAnswer.forEach((item) => {
    for (const [key, value] of Object.entries(item)) {
      if (!totalScores[key]) {
        totalScores[key] = 0;
      }
      totalScores[key] += value;
    }
  });

  let highestScorer = "";

  let val=0

  for (const [key, value] of Object.entries(totalScores)) {
    if (value > val) {
      
      val = value
      highestScorer = key;
    }
  }
  show.value = true
  result.value = highestScorer;
  items.value.results[highestScorer]
};

onBeforeMount(async () => {
  const res = await axios.get(
    `${import.meta.env.VITE_SERVER_URL}/quiz/get-quiz/${route.params.id}`
  );

  if (res.data.data.success) {
    items.value = res.data.data.list;
  }
});
</script>
