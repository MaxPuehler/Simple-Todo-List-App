<template>
  <div>
    <div class="py-4 flex">
      <input
        v-model="todoBody"
        @keyup.enter="todoCreate"
        placeholder="Add your new todo..."
        ref="todoBodyInput"
        class="w-full px-4 py-2 focus:ring-0 bg-gray-300 border-gray-500 border-r-0 rounded-l-lg hover:border-gray-400 focus:outline-0"
        type="text"
      />
      <Datepicker v-model="todoDate" vertical></Datepicker>
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
    utcdate: todoDate.value,
    date: todoDate.value.toDateString(),
    time: todoDate.value.toLocaleTimeString(),
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

function dateFormater(date, separator) {
  var day = date.getDate();
  // add +1 to month because getMonth() returns month from 0 to 11
  var month = date.getMonth() + 1;
  var year = date.getFullYear();

  // show date and month in two digits
  // if month is less than 10, add a 0 before it
  if (day < 10) {
    day = '0' + day;
  }
  if (month < 10) {
    month = '0' + month;
  }

  // now we have day, month and year
  // use the separator to join them
  return day + separator + month + separator + year;
}
</script>
