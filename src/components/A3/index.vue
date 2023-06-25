<template>
  <div class="m-10" v-if="modelValue?.length">
    <div class="slide-box">
      <div class="img-box">
        <div class="box-wrap">
          <img v-for="(image, index) in modelValue" :key="index" :src="image" />
        </div>
      </div>
      <div @click="clickLeft" class="left-arrow arrow">
        <icon icon="ant-design:left-outlined" />
      </div>
      <div @click="clickRight" class="right-arrow arrow">
        <icon icon="ant-design:right-outlined" />
      </div>
      <div class="pagination">
        <span
          v-for="(image, index) in modelValue"
          :key="index"
          @click="current = index"
          @mouseenter="current = index"
          :class="{ active: current === index }"
        ></span>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from "vue";
const props = defineProps({
  modelValue: {
    type: Array,
    default: [],
  },
});
const total = computed(() => props.modelValue.length);

const current = ref(0);
const clickLeft = () => {
  if (current.value > 0) {
    current.value--;
  } else {
    current.value = total.value - 1;
  }
};

const clickRight = () => {
  if (current.value < total.value - 1) {
    current.value++;
  } else {
    current.value = 0;
  }
};

const leftEnable = computed(() => {
  return current.value != 0;
});

const rightEnable = computed(() => {
  return current.value < total.value - 2;
});
</script>

<style lang="scss" scoped>
.slide-box {
  position: relative;
  height: 500px;
  .img-box {
    @apply h-full overflow-hidden;
    .box-wrap {
      @apply flex h-full;
      transition: transform 0.5s ease;
      transform: translateX(calc(-100% * v-bind(current)));
      img {
        @apply w-full flex-shrink-0 h-full;
        object-fit: fill;
      }
    }
  }
  .left-arrow {
    left: 10px;
    transform: translate(-30px, -50%);
  }
  .right-arrow {
    right: 10px;
    transform: translate(30px, -50%);
  }
  .arrow {
    @apply bg-gray-200 rounded-1/2 w-40px h-40px flex justify-center items-center cursor-pointer opacity-0;
    z-index: 10;
    font-weight: bold;
    position: absolute;
    top: 50%;
    filter: drop-shadow(-1px 3px 3px #2a514e);
    transition: all 0.5s ease;
  }
  &:hover {
    .arrow {
      opacity: 0.5;
      transform: translate(0, -50%) !important;
    }
  }
  .pagination {
    @apply flex gap-1 justify-center items-center w-full;
    z-index: 10;
    position: absolute;
    bottom: 10px;
    span {
      @apply w-30px h-3px bg-gray-400 cursor-pointer;
      &.active {
        @apply bg-white;
      }
    }
  }
}
</style>
