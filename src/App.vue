<script setup>
import Input from "./components/Input.vue";
import Todo from "./components/Todo.vue";
import { ref, onBeforeMount, watch } from "vue";

let list = ref([]);

watch(
  list,
  () => {
    localStorage.setItem("list", JSON.stringify(list.value));
  },
  { deep: true }
);

onBeforeMount(() => {
  const storedList = localStorage.getItem("list");
  if (storedList) {
    list.value = JSON.parse(storedList);
  }
});

const handleAdd = (value) => {
  const todo = {
    value,
    done: false,
    createdAt: new Date().getTime(),
  };
  list.value.unshift(todo);
};

const handleUpdate = (value) => {
  list.value = value;
};
</script>

<template>
  <div
    class="w-96 h-screen bg-slate-100 m-auto my-4 p-4 rounded-md font-poppins shadow-md"
  >
    <h2 class="text-3xl font-bold text-slate-700">Todo List</h2>
    <Input @add-list="handleAdd" />
    <Todo :list="list" @update-list="handleUpdate" />
  </div>
</template>
