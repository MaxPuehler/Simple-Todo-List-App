<template>
  <div>
    <div class="py-4 flex">
      <input
        v-model="todoBody"
        @keyup.enter="todoCreate"
        placeholder="Add your new todo..."
        ref="todoBodyInput"
        class="w-full px-4 py-2 focus:ring-0 bg-gray-300 border-gray-500"
        type="text"
      />
      <button
        @click="todoCreate"
        class="px-8 py-2 rounded-r-lg bg-weather-secondary text-white hover:bg-weather-primary transition ease-in-out"
      >
        <i class="fa-solid fa-plus text-xl"></i>
      </button>
    </div>
  </div>
</template>

<script setup>
import { ref } from "@vue/reactivity";

const emit = defineEmits();
const todoBody = ref("");
const todoBodyInput = ref("null");
const todoCreate = () => {
  if (!todoBody.value) {
    return null;
  }
  emit("todoCreate", {
    body: todoBody.value,
    completed: false,
    progress: false,
  });
  todoBody.value = "";
  todoBodyInput.value.focus();
};
</script>
