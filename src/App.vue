<script setup>
import { onMounted, onUnmounted, ref } from "vue";
import MasonryCol from "./components/MasonryCol.vue";

const COL_COUNT = 4;
const SEC_FOR_100PX = 1;
const screenHeight = ref(0);
onMounted(() => {
  window.addEventListener("resize", initScreenHeight);
  initScreenHeight();
});
onUnmounted(() => {
  window.removeEventListener("resize", initScreenHeight);
});
const initScreenHeight = () => {
  screenHeight.value = window.innerHeight;
};

const currentIndex = ref(0);
const dataList = [
  "https://plus.unsplash.com/premium_photo-1661698392174-67a1775e14e5?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1170&q=80",
  "https://images.unsplash.com/photo-1666713533005-3efd57ae59c4?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=688&q=80",
  "https://images.unsplash.com/photo-1666809489316-76eb1f11cb4f?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1632&q=80",
];
const getNewData = (updateFn) => {
  updateFn(dataList[currentIndex.value]);
  const nextIndex = currentIndex.value + 1;
  currentIndex.value = dataList[nextIndex] ? nextIndex : 0;
};
</script>

<template>
  <main class="row">
    <MasonryCol
      v-for="i in COL_COUNT"
      :key="i"
      :screenHeight="screenHeight"
      :secFor100px="SEC_FOR_100PX"
      @getNewData="getNewData"
    />
  </main>
</template>

<style scoped></style>
