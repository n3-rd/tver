<script setup>
import SearchComponent from "./SearchComponent.vue";

// import { onMounted } from "vue";
const getRandomShowId = () => {
  console.log("getting random show");
  localStorage.setItem("showId", Math.floor(Math.random() * 1000));
};
</script>
<template>
  <div class="sidebar flex items-center justify-center w-[20%] fixed">
    <div class="sidebar-inner flex flex-col items-center py-11 gap-6 w-[80%]">
      <SearchComponent />

      <button class="btn gap-2 bg-base-100 w-full" @click="getRandomShowId">
        <svg width="18" height="18" viewBox="0 0 24 24">
          <path
            fill="#c5c9e2"
            d="M5 3h14a2 2 0 0 1 2 2v14a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2V5a2 2 0 0 1 2-2m2 2a2 2 0 0 0-2 2a2 2 0 0 0 2 2a2 2 0 0 0 2-2a2 2 0 0 0-2-2m10 10a2 2 0 0 0-2 2a2 2 0 0 0 2 2a2 2 0 0 0 2-2a2 2 0 0 0-2-2m0-5a2 2 0 0 0-2 2a2 2 0 0 0 2 2a2 2 0 0 0 2-2a2 2 0 0 0-2-2m0-5a2 2 0 0 0-2 2a2 2 0 0 0 2 2a2 2 0 0 0 2-2a2 2 0 0 0-2-2M7 10a2 2 0 0 0-2 2a2 2 0 0 0 2 2a2 2 0 0 0 2-2a2 2 0 0 0-2-2m0 5a2 2 0 0 0-2 2a2 2 0 0 0 2 2a2 2 0 0 0 2-2a2 2 0 0 0-2-2Z"
          />
        </svg>
        Random
      </button>
    </div>
  </div>
</template>
