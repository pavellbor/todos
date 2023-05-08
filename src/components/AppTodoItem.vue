<template>
  <li class="todo-item" :class="{'todo-item--done': todo.completed}" @click="toggleTodo">
    <div class="todo-item__status">
      <i class="bi bi-check2"></i>
    </div>
    <span class="todo-item__text">{{ todo.text }}</span>
    <button class="todo-item__remove-button" @click.stop="removeTodo">
      <i class="bi bi-trash3"></i>
    </button>
  </li>
</template>

<script lang="ts">
import { Todo } from '@/types/Todo';
import { PropType, defineComponent } from 'vue';

export default defineComponent({
  props: {
    todo: {
      type: Object as PropType<Todo>,
      required: true,
    }
  },
  methods: {
    toggleTodo() {
      this.$emit('toggleTodo', this.todo.id)
    },
    removeTodo() {
      this.$emit('removeTodo', this.todo.id)
    }
  },
  emits: {
    toggleTodo: (id: number) => Number.isInteger(id),
    removeTodo: (id: number) => Number.isInteger(id),
  }
})
</script>