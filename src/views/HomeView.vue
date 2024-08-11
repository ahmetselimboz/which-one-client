<template>
  <div class="bg-pink-50 w-full h-full pb-10">
    <HomeViewHeader />
    <div class="lg:px-8 px-4 py-2 w-5/6 mx-auto">
      <div class="w-full flex flex-wrap items-center justify-between gap-4">
        <template v-for="item in items">
          <HomeViewCard :item="{ item }" />
        </template>
      </div>
    </div>
  </div>
</template>

<script setup>
import HomeViewHeader from "../components/HomeView_Header.vue";
import HomeViewCard from "../components/HomeView_Card.vue";
import { onBeforeMount, onBeforeUnmount, onMounted, ref } from "vue";
import axios from "axios";

const items = ref([]);

onBeforeMount(async () => {
  const res = await axios.get(
    `${import.meta.env.VITE_SERVER_URL}/quiz/get-all-list`
  );

  if (res.data.data.success) {
    items.value = res.data.data.list;
  }

});
</script>
