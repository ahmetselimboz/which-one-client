<template>
  <div class="w-full lg:h-3/5 h-1/3 py-12 flex flex-col items-center justify-end">
    <div
      class="text-violet-700 font-bold lg:text-8xl  text-6xl my-10 font-bubblegum"
    
    >
      Hangisisin?
    </div>
    <div class="w-full flex flex-col items-center">
      <div
        class="lg:w-1/3 w-2/3 h-12 rounded-full overflow-hidden border-2 border-black/20 flex flex-row items-center"
      >
        <input
          type="text"
          class="outline-none w-full py-2 px-4 lg:text-lg text-sm poppins-regular text-gray-600"
          placeholder="Ara..."
        />
        <button
          class="bg-indigo-500 hover:bg-indigo-600 transition-all poppins-regular h-full px-4 text-white flex flex-row items-center gap-2 lg:text-lg text-sm"
        >
          <i class="pi pi-search lg:text-lg text-sm"></i>Ara
        </button>
      </div>
    </div>
  </div>
</template>

<script setup></script>
