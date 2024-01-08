<script setup>
import FormTodo from './FormTodo.vue';
import StatusTodo from './StatusTodo.vue';
import Todo from './Todo.vue';
</script>

<template>
  <div class="todo-list w-[900px] flex flex-col gap-5 max-w-md mx-auto">
    <p class="text-2xl text-center sm:text-left font-bold">TODO APP</p>
    <StatusTodo />
    <FormTodo />
    <Todo />
  </div>
</template>

<script>
  
</script>