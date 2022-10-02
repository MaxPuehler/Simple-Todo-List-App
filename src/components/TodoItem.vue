<template>
  <div
    class="flex justify-center px-4 py-2 border-b border-gray-300 hover:bg-indigo-50 group"
  >
    <div
      class="flex items-center font-Roboto text-lg font-medium cursor-pointer"
    >
      <div>
        <input
          id="default-checkbox"
          type="checkbox"
          v-if="todo.priority === 0"
          v-model="todo.completed"
          class="w-4 h-4 rounded border-gray-500 focus:ring-0 border-2"
        />
      </div>
      <div>
        <input
          id="default-checkbox"
          type="checkbox"
          v-if="todo.priority === 1"
          v-model="todo.completed"
          class="w-4 h-4 rounded border-blue-500 focus:ring-0 border-2"
        />
      </div>
      <div>
        <input
          id="default-checkbox"
          type="checkbox"
          v-if="todo.priority === 2"
          v-model="todo.completed"
          class="w-4 h-4 rounded border-yellow-300 focus:ring-0 border-2"
        />
      </div>
      <div>
        <input
          id="default-checkbox"
          type="checkbox"
          v-if="todo.priority === 3"
          v-model="todo.completed"
          class="w-4 h-4 rounded border-red-500 focus:ring-0 border-2"
        />
      </div>
      <div class="mx-3">
        <div
          @click="todoToggle(todo)"
          :class="{
            'bg-gray-100': todo.completed,
            'text-gray-400': todo.completed,
            'line-through': todo.completed,
          }"
        >
          {{ todo.body }}
        </div>
        <div class="text-xs text-gray-500">
          <i class="fa-regular fa-calendar"></i>
          {{ todo.date }} {{ todo.time }}
        </div>
      </div>
    </div>
    <div class="flex gap-6 ml-auto">
      <button
        @click="toggleModal()"
        v-bind="index"
        class="text-gray-500 invisible group-hover:visible"
      >
        . . .
      </button>
      <div
        @click="todoToggleProgress(todo)"
        v-if="(todo.progress === true) & (todo.completed === false)"
        class="flex p-1 border rounded-md text-yellow-400 border-yellow-300"
      >
        <button class="font-medium">In progress</button>
      </div>
      <div
        v-if="(todo.progress === false) & (todo.completed === false)"
        @click="todoToggleProgress(todo)"
        class="flex p-1 border rounded-md border-gray-400 text-gray-500"
      >
        <button class="font-medium">Todo</button>
      </div>

      <div
        v-if="todo.completed === true"
        class="flex p-1 border rounded-md border-green-600 text-green-600"
      >
        <button class="text-m font-medium">Completed</button>
      </div>
      <button
        class="text-xl text-gray-400 hover:text-red-600 focus:ring-0"
        @click="todoRemove(index)"
      >
        <i class="fa-sharp fa-solid fa-xmark"></i>
      </button>
    </div>
  </div>
  <TodoModal :modalActive="modalActive" @close-modal="toggleModal" class="z-10">
    <ul class="font-Roboto">
      <li class="py-2">
        <p>Edit Todo:</p>
        <input
          :value="todo.body"
          @input="(event) => (todo.body = event.target.value)"
          class="bg-gray-300 w-full p-2 border border-gray-500 focus:ring-0 focus:ring-weather-primary focus"
        />
      </li>
      <li class="py-2">
        <p>Edit Date:</p>
        <Datepicker
        v-model="todo.utcdate"
        @input="(event) => (todo.utcdate = event.target.value)"
          vertical
          ref="todoDateInput"
        ></Datepicker>
      </li>

      <li class="py-2"><p>Choose Priority:</p></li>
      <div>
        <ul class="flex justify-between">
          <li>
            <button
              @click="todoPrio1(todo)"
              class="w-7 h-7 border border-gray-500 rounded-md hover:bg-indigo-100"
            >
              <i class="fa-regular fa-flag text-red-700"></i>
            </button>
          </li>
          <li>
            <button
              @click="todoPrio2(todo)"
              class="w-7 h-7 border border-gray-500 rounded-md hover:bg-indigo-100"
            >
              <i class="fa-regular fa-flag text-yellow-300"></i>
            </button>
          </li>
          <li>
            <button
              @click="todoPrio3(todo)"
              class="w-7 h-7 border border-gray-500 rounded-md hover:bg-indigo-100"
            >
              <i class="fa-regular fa-flag text-blue-500 "></i>
            </button>
          </li>
          <li>
            <button
              @click="todoPrio4(todo)"
              class="w-7 h-7 border border-gray-500 rounded-md hover:bg-indigo-100"
            >
              <i class="fa-regular fa-flag text-black"></i>
            </button>
          </li>
        </ul>
      </div>
    </ul>
  </TodoModal>
</template>

<script setup>
import { ref } from "vue";
import TodoModal from "./TodoModal.vue";
import Datepicker from "@vuepic/vue-datepicker";
import "@vuepic/vue-datepicker/src/VueDatePicker/style/main.scss";

const emit = defineEmits();

defineProps({
  index: {
    type: Number,
    required: true,
  },
  todo: {
    body: {
      type: String,
      required: true,
    },
    utc: {
      type: String,
      required: false,
    },
    date: {
      type: String,
      required: false,
    },
    time: {
      type: String,
      required: false,
    },
    completed: {
      type: Boolean,
      required: true,
    },
    progress: {
      type: Boolean,
      required: true,
    },
    priority: {
      type: Number,
      required: true,
    },
  },
});

const todoRemove = (index) => {
  emit("todoRemove", index);
};

const todoToggle = (todo) => {
  todo.completed = !todo.completed;
};

const todoToggleProgress = (todo) => {
  todo.progress = !todo.progress;
};

const modalActive = ref(null);
const toggleModal = () => {
  modalActive.value = !modalActive.value;
};

const todoPrio1 = (todo) => {
  todo.priority = 3;
};

const todoPrio2 = (todo) => {
  todo.priority = 2;
};

const todoPrio3 = (todo) => {
  todo.priority = 1;
};

const todoPrio4 = (todo) => {
  todo.priority = 0;
};
</script>
