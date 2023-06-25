<template>
  <div class="m-10">
    <div class="input-box mb-5">
      <input v-model="text" @keyup.enter="doAdd" />
      <icon
        icon="carbon:close-filled"
        class="text-black"
        v-if="text"
        @click="text = ''"
      />
      <button :disabled="!text" @click="doAdd">Add</button>
    </div>
    <TransitionGroup tag="ul" name="list" class="list">
      <li
        v-for="(item, index) in list"
        :key="item"
        @click="list.splice(index, 1)"
      >
        {{ item }}
      </li>
    </TransitionGroup>
  </div>
</template>

<script setup>
import { ref, watch, onBeforeMount } from "vue";
const props = defineProps(["modelValue"]);
const emits = defineEmits(["update:modelValue"]);
const text = ref("");
const list = ref([]);
onBeforeMount(() => {
  list.value = props.modelValue;
});
watch(props.modelValue, (newValue) => {
  emits("update:modelValue", newValue);
});
const doAdd = () => {
  if (!text.value) {
    return;
  }
  list.value.push(text.value);
  text.value = "";
};
</script>

<style lang="scss" scoped>
.input-box {
  @apply rounded flex items-center w-500px bg-black overflow-hidden relative;
  input {
    @apply flex-1 p-1 rounded bg-white m-1 pr-30px;
    &:focus {
      outline: none;
    }
  }
  .iconify {
    @apply absolute cursor-pointer;
    right: 110px;
    top: calc(50% - 8px);
  }
  button {
    @apply flex-0 bg-black p-2 text-white w-100px;
    &:disabled {
      cursor: not-allowed;
    }
  }
}

.list {
  @apply m-5 inline-flex flex-col;
  list-style: none;
  li {
    @apply relative cursor-pointer;
    &::before {
      @apply w-5px h-5px bg-black rounded-1/2 absolute;
      left: -10px;
      top: calc(50% - 2px);
      content: "";
    }
    &:hover {
      text-decoration: line-through;
    }
  }
  &-enter-active,
  &-leave-active {
    transition: all 0.5s ease;
    // position: absolute;
  }
  &-enter-from {
    opacity: 0;
    transform: translateY(30px);
  }
  &-leave-to {
    opacity: 0;
    transform: translateX(30px);
  }
}
</style>
