<template>
  <div
    class="flex justify-center px-4 py-2 border-b border-gray-300 hover:bg-indigo-50"
  >
    <div
      class="flex items-center gap-2 font-Roboto font-medium"
      @click="todoToggle(todo)"
      :class="{
        'bg-gray-100': todo.completed,
        'text-gray-400': todo.completed,
        'line-through': todo.completed,
      }"
    >
      <div>
        <input
          id="default-checkbox"
          type="checkbox"
          v-model="todo.completed"
          class="w-4 h-4 rounded border-gray-300 focus:ring-blue-500 dark:focus:ring-blue-600 focus:ring-0 dark:border-gray-400 border-2"
        />
      </div>
      {{ todo.body }}
    </div>

    <div class="flex gap-6 ml-auto">
      <div
        @click="todoToggleProgress(todo)"
        v-if="(todo.progress === true) & (todo.completed === false)"
        class="p-1 border rounded-md text-yellow-400 border-yellow-300"
      >
        <button class="text-m font-medium">In progress</button>
      </div>
      <div
        v-if="(todo.progress === false) & (todo.completed === false)"
        @click="todoToggleProgress(todo)"
        class="p-1 border rounded-md border-gray-400 text-gray-500"
      >
        <button class="text-m font-medium">Todo</button>
      </div>

      <div
        v-if="todo.completed === true"
        class="p-1 border rounded-md border-green-600 text-green-600"
      >
        <button class="text-m font-medium">Completed</button>
      </div>
      <button
        class="text-xl text-gray-400 hover:text-red-600 focus:ring-0"
        @click.stop="todoRemove(index)"
      >
        <i class="fa-sharp fa-solid fa-xmark"></i>
      </button>
    </div>
  </div>
</template>

<script setup>
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
    completed: {
      type: Boolean,
      required: true,
    },
    progress: {
      type: Boolean,
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
</script>
