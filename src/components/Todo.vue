<script setup>
import { ref, watch, defineEmits, defineProps, onMounted } from "vue";
const props = defineProps(["list"]);
const emit = defineEmits(["update-list"]);
const lists = ref([]);

onMounted(() => {
  lists.value = props.list;
});

watch(
  lists,
  (newValue) => {
    lists.value = newValue;
    emit("update-list", newValue);
  },
  { deep: true }
);

const deleteList = (indexList) => {
  const newList = lists.value.filter((value, index) => {
    return index != indexList;
  });
  lists.value = newList;
};
</script>

<template>
  <section class="h-5/6 mt-4 overflow-y-auto">
    <div
      class="flex justify-between w-full mb-3 bg-white p-3 rounded"
      v-for="(list, index) in lists"
    >
      <div class="flex justify-between">
        <div class="flex gap-2">
          <input
            id="default-checkbox"
            type="checkbox"
            :checked="list.done"
            v-model="list.done"
            class="w-4 text-blue-600 bg-gray-100 border-gray-300 rounded focus:ring-blue-500 dark:focus:ring-blue-600 dark:ring-offset-gray-800 focus:ring-2 dark:bg-gray-700 dark:border-gray-600"
          />
          <input
            type="text"
            class="focus:outline-none w-11/12"
            v-model="list.value"
          />
        </div>
      </div>
      <button
        type="submit"
        @click="deleteList(index)"
        class="p-1 ml-2 mr-2 text-sm font-medium text-white bg-red-700 rounded-lg border border-red-700 hover:bg-red-800"
      >
        Delete
      </button>
    </div>
  </section>
</template>
