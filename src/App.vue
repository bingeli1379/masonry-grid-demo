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
  "https://images.unsplash.com/photo-1492571350019-22de08371fd3?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1053&q=80",
  "https://images.unsplash.com/photo-1480796927426-f609979314bd?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1170&q=80",
  "https://images.unsplash.com/photo-1528164344705-47542687000d?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1192&q=80",
  "https://images.unsplash.com/photo-1542051841857-5f90071e7989?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1170&q=80",
  "https://images.unsplash.com/photo-1601823984263-b87b59798b70?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=687&q=80",
  "https://images.unsplash.com/photo-1554797589-7241bb691973?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=736&q=80",
  "https://images.unsplash.com/photo-1542931287-023b922fa89b?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=687&q=80",
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
