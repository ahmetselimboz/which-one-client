<template>
  <div class="bg-pink-50 w-full h-full pb-10">
    <HomeViewHeader @changedItems="itemsFunc" />
    <div class="lg:px-8 px-4 py-2 w-5/6 mx-auto">
      <div class="w-full flex flex-wrap items-center justify-between gap-4">
        <template v-for="item in items" :key="item._id">
          <HomeViewCard :item="{ item }" />
        </template>
      </div>
    </div>
  </div>
  <span class="hidden">{{ computedItems }}</span>
</template>

<script setup>
import HomeViewHeader from "../components/HomeView_Header.vue";
import HomeViewCard from "../components/HomeView_Card.vue";
import { computed, onBeforeMount, onBeforeUnmount, onMounted, ref } from "vue";
import axios from "axios";

const items = ref([]);
const data = ref([]);
const inputText = ref("");

onMounted(async () => {
  try {
    const res = await axios.get(
      `${import.meta.env.VITE_SERVER_URL}/quiz/get-all-list`
    );

    if (res.data.data.success) {
      items.value = res.data.data.list;
      data.value = items.value;
    }
  } catch (error) {
    console.error("Error fetching quiz list:", error);
  }
});

const itemsFunc = (e) => {
  inputText.value = e;
};

const computedItems = computed(() => {
  return (items.value = data.value.filter((item) =>
    item.title.toLowerCase().includes(inputText.value.toLowerCase())
  ));
});
</script>
