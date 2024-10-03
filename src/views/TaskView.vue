<script setup>
import { ref, watch, onMounted } from 'vue'

const taskInputs = ref([''])
const taskInput = ref('')
const errors = ref({
  task: ''
})

const addTask = () => {
  errors.value = {
    task: ''
  }

  if (taskInput.value.trim() === '') {
    errors.value.task = 'Please enter task !!!'
  } else {
    taskInputs.value.unshift(taskInput.value)
    taskInput.value = ''
  }
}

const deleteTask = (index) => {
  taskInputs.value.splice(index, 1)
}

watch(
  taskInputs,
  (newTaskInputs) => {
    localStorage.setItem('taskInputs', JSON.stringify(newTaskInputs))
  },
  { deep: true }
)

onMounted(() => {
  taskInputs.value = JSON.parse(localStorage.getItem('taskInputs')) || []
})

// // Watch for changes in taskInputs and update localStorage
// watch(taskInputs, (newTaskInputs) => {
//   localStorage.setItem('taskInputs', JSON.stringify(newTaskInputs))
// }, { deep: true })  // Ensure deep watching in case taskInputs is a complex object or array

// // Set the taskInputs from localStorage when the component is mounted
// onMounted(() => {
//   const savedTasks = localStorage.getItem('taskInputs')
//   taskInputs.value = savedTasks ? JSON.parse(savedTasks) : []
// })
</script>

<template>
  <div class="grid place-items-center">
    <div class="p-10 flex gap-2">
      <div>
        <input
          type="text"
          placeholder="Input task here..."
          v-model="taskInput"
          class="border p-2 focus:outline-none focus:ring rounded w-80"
        />
        <div v-if="errors.task" class="text-red-500 text-sm">{{ errors.task }}</div>
      </div>
      <button
        @click="addTask"
        class="p-2 w-20 h-11 border bg-blue-500 text-white rounded-lg hover:bg-pink-500 duration-300"
      >
        Add
      </button>
    </div>
    <div class="task-list">
      <div v-for="(task, index) in taskInputs" :key="task" class="flex gap-2 my-2">
        <div class="bg-blue-100 w-60 rounded-lg">
          <p class="p-2 flex-grow w-full">{{ task }}</p>
        </div>
        <button
          @click="deleteTask(index)"
          class="border p-2 rounded-lg bg-orange-600 text-white hover:bg-orange-400 duration-300"
        >
          Delete
        </button>
      </div>
    </div>
  </div>
</template>
