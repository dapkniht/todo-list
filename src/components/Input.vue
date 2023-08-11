<script setup>
import { ref, watch, onMounted, defineEmits } from "vue";
const emit = defineEmits(["add-list"]);
const input = ref("");

onMounted(() => {
  input.value = localStorage.getItem("input");
});

watch(input, (newValue) => {
  localStorage.setItem("input", newValue);
});

const storeInput = () => {
  emit("add-list", input.value);
  input.value = "";
};
</script>

<template>
  <section class="mt-4">
    <form class="flex items-center" @submit.prevent="storeInput">
      <input
        v-model="input"
        type="text"
        id="voice-search"
        class="bg-white border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5"
        placeholder="Add your todo here..."
        required
      />
      <button
        type="submit"
        class="inline-flex items-center py-2.5 px-3 ml-2 text-sm font-medium text-white bg-blue-700 rounded-lg border border-blue-700 hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300"
      >
        Add
      </button>
    </form>
  </section>
</template>
