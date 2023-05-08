<template>
  <section class="add-todo">
    <form
      v-if="isFormVisible"
      class="add-todo__form"
      @submit.prevent="addTodo"
    >
      <button
        class="close-button"
        type="button"
        @click="closeForm"
      >
        <i class="bi bi-x"></i>
      </button>
      <div class="text-input text-input--focus">
        <input v-model="todoText" class="input" />
      </div>
      <button class="button button--filled">Add task</button>
    </form>
    <button
      v-else
      class="add-todo__show-form-button"
      @click="showForm"
    >
      <i class="bi bi-plus-lg"></i>
    </button>
  </section>
</template>

<script lang="ts">
import { Todo } from '@/types/Todo';
import { defineComponent } from 'vue';

interface State {
  isFormVisible: boolean,
  todoText: string
}

export default defineComponent({
  data(): State {
    return {
      isFormVisible: false,
      todoText: '',
    }
  },
  methods: {
    showForm() {
      this.isFormVisible = true
    },
    closeForm() {
      this.isFormVisible = false
    },
    addTodo() {
      this.$emit('addTodo', {
        id: Date.now(),
        text: this.todoText,
        completed: false,
      })

      this.todoText = ''
    }
  },
  emits: {
    addTodo: (todo: Todo) => todo
  }
})
</script>