<template>
  <div>
    <div class="text-center text-lime-400 bg-black tracking-wide">
      面试官老师您好，感谢您百忙之中抽空来检阅我的面试实践题 这是我的<a
        href="https://lovehin.github.io/my-resume/"
        class="underline mx-1 tracking-wide"
        >个人简历</a
      >
    </div>
    <p class="question">
      请实现一个 Vue
      组件，包含一个输入框和一个按钮，点击按钮后将输入框中的内容添加到一个列表中。
    </p>
    <A1 v-model="list" />
    <p class="question">
      请实现一个 Vue
      组件，包含一个输入框和一个表格，输入框中输入关键字后，表格中的数据会根据关键字进行筛选。
    </p>
    <A2 />
    <p class="question">
      请实现一个 Vue
      组件，包含一个轮播图和一个分页器，轮播图中有多张图片，分页器可以切换轮播图中的图片。
    </p>
    <A3 v-model="images" />
    <p class="question">
      请实现一个 Vue 组件，包含一个按钮和一个 modal 弹框， 点击按钮出现 modal
      框，点击其他部分 modal 框消失。在该组件基础上，使其支持自定义 modal
      框内容，头部和底部。
    </p>
    <div class="flex gap-5 justify-center my-10">
      <button
        @click="visible[0] = true"
        class="border border-gray-100 p-1 bg-black text-white rounded"
      >
        空白 对话框
      </button>
      <button
        @click="visible[1] = true"
        class="border border-gray-100 p-1 bg-black text-white rounded"
      >
        有标题 对话框
      </button>
      <button
        @click="visible[2] = true"
        class="border border-gray-100 p-1 bg-black text-white rounded"
      >
        自定义header 对话框
      </button>
      <button
        @click="visible[3] = true"
        class="border border-gray-100 p-1 bg-black text-white rounded"
      >
        无header 对话框
      </button>
      <button
        @click="visible[4] = true"
        class="border border-gray-100 p-1 bg-black text-white rounded"
      >
        自定义footer 对话框
      </button>
    </div>
    <A4 v-model="visible[0]"> </A4>
    <A4 v-model="visible[1]" title="有标题">
      <div class="p-5 text-center">我是内容</div>
    </A4>
    <A4 v-model="visible[2]">
      <template #header>
        <div class="p-5 text-center font-bold text-lg">自定义标题</div>
      </template>
      <div class="p-5 text-center">我是内容</div>
    </A4>
    <A4 v-model="visible[3]" noHeader>
      <div class="p-5 text-center">我是内容</div>
    </A4>
    <A4 v-model="visible[4]" title="有底部对话框">
      <div class="p-5 text-center">我是内容</div>
      <template #footer>
        <div class="flex justify-between px-10 py-5 border-t border-gray-100">
          <button class="border rounded border-gray-200 bg-gray-200 p-1">
            取 消
          </button>
          <button
            class="border rounded border-gray-200 bg-blue-500 p-1 text-white"
          >
            确 认
          </button>
        </div>
      </template>
    </A4>
  </div>
</template>

<script setup>
import { ref } from "vue";
import A1 from "@/components/A1/index.vue";
import A2 from "@/components/A2/index.vue";
import A3 from "@/components/A3/index.vue";
import A4 from "@/components/A4/index.vue";
const list = ref([1, 2, 3]);
const images = ref([
  "https://tse1-mm.cn.bing.net/th/id/OIP-C.R7mq1Wy9RO5SZBaAhkC5_AHaEo?w=274&h=180&c=7&r=0&o=5&dpr=2&pid=1.7",
  "https://tse1-mm.cn.bing.net/th/id/OIP-C.82ZW_gKmRaPVUkAGu1c7HQHaEo?w=275&h=180&c=7&r=0&o=5&dpr=2&pid=1.7",
  "https://tse3-mm.cn.bing.net/th/id/OIP-C.g9UbVfyVZX-SfD09JcYr5QHaEK?w=245&h=180&c=7&r=0&o=5&dpr=2&pid=1.7",
  "https://tse1-mm.cn.bing.net/th/id/OIP-C.SEnf6RFSsoBKFSeVTJzDxwHaEK?w=290&h=180&c=7&r=0&o=5&dpr=2&pid=1.7",
  "https://tse2-mm.cn.bing.net/th/id/OIP-C.2QpKqRTIVw_n-9Ubqq-tOwHaEK?w=276&h=180&c=7&r=0&o=5&dpr=2&pid=1.7",
  "https://tse3-mm.cn.bing.net/th/id/OIP-C.FelwzQdlCWF4ptoWmTz7sQHaEK?w=272&h=180&c=7&r=0&o=5&dpr=2&pid=1.7",
]);
const visible = ref(new Array(10).fill(false));
</script>

<style lang="scss" scoped>
.question {
  @apply bg-gray-200 inline-block p-1 mt-5 mb-2;
  border-top-right-radius: 10px;
  border-bottom-right-radius: 10px;
}
</style>
