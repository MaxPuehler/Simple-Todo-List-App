<template>
  <div>
    <div class="py-4 flex">
      <input
        v-model="todoBody"
        @keyup.enter="todoCreate"
        placeholder="Add your new todo..."
        ref="todoBodyInput"
        class="w-full px-4 py-2 focus:ring-0 bg-gray-300 border-gray-500 border-r-0 rounded-l-lg hover:border-gray-400 focus:outline-0 placeholder-gray-500"
        type="text"
      />
      <Datepicker
        v-model="todoDate"
        vertical
        model-type="EEEE, LLL dd HH:mm"
        placeholder="Select Date"
      ></Datepicker>
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
import Datepicker from "@vuepic/vue-datepicker";
import "@vuepic/vue-datepicker/src/VueDatePicker/style/main.scss";
import TodoItem from "./TodoItem.vue";

const emit = defineEmits();
const todoBody = ref("");
const todoDate = ref("");
const todoBodyInput = ref("null");

const todoCreate = () => {
  if (!todoBody.value) {
    return null;
  }
  emit("todoCreate", {
    body: todoBody.value,
    completed: false,
    progress: false,
    priority: 0,
    date: todoDate.value,
  });
  todoBody.value = "";
  todoBodyInput.value.focus();
  todoDate.value = "";
};

const truncate = (text, length) => {
  if (text.length > length) {
    return text.substring(0, length);
  } else {
    return text;
  }
};
</script>
