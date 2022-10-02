<template>
  <div>
    <header class="sticky top-0 bg-weather-primary shadow-xl z-10">
      <div
        class="flex justify-center items-center gap-3 mx-auto text-center text-3xl text-white py-6 font-Roboto"
      >
        <i class="fa-regular fa-circle-check"></i>
        <h1>What Todo?</h1>
      </div>
    </header>
    <main class="absolute min-h-screen w-full bg-cover bg-weather-primary">
      <div class="max-w-xl my-10 p-7 mx-auto rounded-xl bg-white">
        <TodoItem
          v-for="(todo, index) in todos"
          :todo="todo"
          v-bind:key="todo.index"
          :index="index"
          @todoRemove="todoRemove"
        ></TodoItem>
        <TodoCreate @TodoCreate="todoCreate" />
        <div class="mt-3 mx-auto">
          <button
            @click="todoClearCompleted"
            class="px-6 py-2 bg-weather-secondary hover:bg-weather-primary text-white rounded"
          >
            Clear completed tasks
          </button>
        </div>
      </div>
    </main>
  </div>
</template>

<script setup>
import { ref } from "@vue/reactivity";
import TodoItem from "./TodoItem.vue";
import TodoCreate from "./TodoCreate.vue";
import TodoModal from "./TodoModal.vue";

const todos = ref([]);

const todoCreate = (todo) => {
  todos.value = [...todos.value, todo];
};

const todoRemove = (index) => {
  todos.value.splice(index, 1);
};

const todoClearCompleted = () => {
  todos.value = [
    ...todos.value.filter((todo) => {
      return !todo.completed;
    }),
  ];
};
</script>
