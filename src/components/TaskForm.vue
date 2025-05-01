<script lang="ts" setup>
import { ref } from "vue";

// Component logic is already handled by <script setup>, no need for default export
const emit = defineEmits<{
  addTask: [newTask: string];
}>();

const newTask = ref("");
const error = ref("");

const formSubmitted = () => {
  if (newTask.value.trim()) {
    // Prevent submission if the input is empty
    // Emit the new task value to the parent component
    emit("addTask", newTask.value.trim()); // Emit the new task value to the parent component
    newTask.value = ""; // Clear the input after submission
  } else {
    error.value = "Task Cannot be Empty!";
  }
};
</script>

<template>
  <form @submit.prevent="formSubmitted">
    <label for=""
      >New Task<input
        v-model="newTask"
        type="text"
        name="newTask"
        :aria-invalid="!!error || undefined"
        @input="error = ''"
      />
      <small v-if="error" id="invalid-helper">{{ error }} </small>
    </label>
    <div class="button-container">
      <button>Add</button>
    </div>
  </form>
</template>
