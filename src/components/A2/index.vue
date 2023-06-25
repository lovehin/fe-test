<template>
  <div class="m-10">
    <div class="input-box mb-5">
      <input v-model="text" placeholder="输入关键词" />
      <icon
        icon="carbon:close-filled"
        class="text-black"
        v-if="text"
        @click="text = ''"
      />
    </div>
    <table>
      <thead>
        <tr>
          <th>ID</th>
          <th>姓名</th>
          <th>年龄</th>
          <th>性别</th>
          <th>职业CN</th>
          <th>职业EN</th>
        </tr>
      </thead>
      <tbody id="tbody">
        <tr v-for="person in filteredPersons" :key="person.id">
          <td v-html="highlight(person.id)"></td>
          <td v-html="highlight(person.name)"></td>
          <td v-html="highlight(person.age)"></td>
          <td v-html="highlight(person.gender)"></td>
          <td v-html="highlight(person.occupation)"></td>
          <td v-html="highlight(person.occupation_en)"></td>
        </tr>
        <tr v-if="filteredPersons.length === 0">
          <td colspan="6" class="!text-center !p-10">暂无符合关键词的数据</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

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
    right: 10px;
    top: calc(50% - 8px);
  }
}
table {
  @apply border border-gray-100 w-full shadow;
  border-collapse: collapse;
  th {
    @apply bg-black text-white;
  }
  th,
  td {
    @apply p-1 text-left border-gray-100 border;
  }
  tr:nth-child(even) {
    td {
      @apply bg-gray-200;
    }
  }
}
</style>

<script setup>
import { ref, computed } from "vue";

const text = ref("");
const persons = ref([
  {
    id: 1,
    name: "张三",
    age: 20,
    gender: "男",
    occupation: "学生",
    occupation_en: "Student",
  },
  {
    id: 2,
    name: "李四",
    age: 25,
    gender: "女",
    occupation: "教师",
    occupation_en: "Teacher",
  },
  {
    id: 3,
    name: "王五",
    age: 30,
    gender: "男",
    occupation: "工程师",
    occupation_en: "Engineer",
  },
  {
    id: 4,
    name: "赵六",
    age: 28,
    gender: "女",
    occupation: "医生",
    occupation_en: "Doctor",
  },
  {
    id: 5,
    name: "钱七",
    age: 35,
    gender: "男",
    occupation: "律师",
    occupation_en: "Lawyer",
  },
  {
    id: 6,
    name: "孙八",
    age: 22,
    gender: "女",
    occupation: "设计师",
    occupation_en: "Designer",
  },
  {
    id: 7,
    name: "周九",
    age: 27,
    gender: "男",
    occupation: "销售员",
    occupation_en: "Salesman",
  },
  {
    id: 8,
    name: "吴十",
    age: 33,
    gender: "女",
    occupation: "会计",
    occupation_en: "Accountant",
  },
  {
    id: 9,
    name: "郑十一",
    age: 29,
    gender: "男",
    occupation: "经理",
    occupation_en: "Manager",
  },
  {
    id: 10,
    name: "王十二",
    age: 31,
    gender: "女",
    occupation: "演员",
    occupation_en: "Actor",
  },
]);
const filteredPersons = computed(() => {
  if (!text.value) {
    return persons.value;
  }
  return persons.value.filter((person) =>
    Object.values(person).some((i) => {
      const t = i.toString();
      return t.toLowerCase().includes(text.value.toLowerCase());
    })
  );
});
const highlight = (value) => {
  const innerText = value.toString();
  if (!text.value) {
    return innerText;
  }
  const re = new RegExp(`(${text.value})`, "gi");
  if (innerText.match(re)) {
    return innerText.replace(re, '<span class="text-red-500">$1</span>');
  } else {
    return innerText;
  }
};
</script>
