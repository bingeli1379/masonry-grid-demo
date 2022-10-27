<script setup>
import { nextTick, onMounted, ref } from "vue";

const props = defineProps({
  screenHeight: {
    type: Number,
    required: true,
  },
  secFor100px: {
    type: Number,
    required: true,
  },
});
const emit = defineEmits(["getNewData"]);

const wrap = ref(null);
const dataList = ref([]);
onMounted(() => {
  checkItemLength();
  startAnimation();
});

const checkItemLength = () => {
  const firstItem = wrap.value.children[0];
  const firstItemHeight = firstItem ? firstItem.offsetHeight : 0;
  const minHeight = props.screenHeight + firstItemHeight;
  if (wrap.value.offsetHeight > minHeight) return;
  emit("getNewData", addData);
};
let id = 1;
const addData = (url) => {
  dataList.value.push({
    id: id++,
    url,
  });
};

let move = 0;
const startAnimation = () => {
  const firstItem = wrap.value.children[0];
  const firstItemHeight = firstItem ? firstItem.offsetHeight : 0;
  let start = null;
  function step(timestamp) {
    const time = start ? timestamp - start : 0;
    start = timestamp;
    move += (time / 10) * props.secFor100px;
    wrap.value.style.top = `-${move}px`;
    if (move >= firstItemHeight) {
      move -= firstItemHeight;
      dataList.value.shift();
      wrap.value.style.top = `-${move}px`;
      nextTick(checkItemLength);
      return;
    }
    window.requestAnimationFrame(step);
  }
  window.requestAnimationFrame(step);
};
</script>

<template>
  <div class="col" ref="wrap">
    <div v-for="data in dataList" :key="data.id">
      <img :src="data.url" @load="checkItemLength" />
    </div>
  </div>
</template>

<style scoped>
.col {
  position: relative;
}
</style>
