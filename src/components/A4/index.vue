<template>
  <Transition name="overlay">
    <div class="overlay" @click.self="doClose" v-if="modelValue">
      <div class="dialog">
        <slot name="header">
          <div class="header" v-if="!noHeader">
            <span class="title">{{ title }}</span>
            <button @click="doClose">X</button>
          </div>
        </slot>
        <div class="content">
          <slot />
        </div>
        <div class="footer">
          <slot name="footer"> </slot>
        </div>
      </div>
    </div>
  </Transition>
</template>

<script setup>
const props = defineProps({
  modelValue: {
    type: Boolean,
    default: false,
  },
  title: {
    type: String,
    default: "",
  },
  width: {
    type: Number,
    default: 50,
  },
  noHeader: {
    type: Boolean,
    default: false,
  },
});
const emits = defineEmits(["update:modelValue"]);
const doClose = () => {
  emits("update:modelValue", false);
};
</script>

<style lang="scss" scoped>
.overlay {
  @apply fixed top-0 left-0 right-0 bottom-0 bg-black bg-opacity-40 flex justify-center items-center;
  z-index: 9999;
  &-enter-active,
  &-leave-active {
    transition: all 0.2s ease;
  }

  &-enter-from {
    transform: translateY(-100%);
  }
  &-leave-to {
    transform: translateY(-100%);
  }
  .dialog {
    @apply bg-white rounded shadow;
    width: calc(v-bind(width) * 1%);
    .header {
      @apply flex justify-between items-center p-5;
      .title {
        @apply text-lg text-gray-800;
      }
      button {
        @apply text-gray-500;
        &:hover {
          @apply text-blue-400;
        }
      }
    }

    .content {
      @apply p-5;
    }
  }
}
</style>
