<script setup>
import CompletedTodo from './CompletedTodo.vue';
import UncompletedTodo from './UncompletedTodo.vue';

</script>


<template>
      <div class="todos flex flex-wrap justify-between gap-7 lg:gap-3 w-full">
        <div class="todo-not-completed w-full">
          <h3 class="text-left font-bold text-xl pb-3">TODO</h3>
          <div class="text-center font-bold py-20" v-if="emptyTodo"> </div>
          <!-- TODO UNCOMPLETED -->
          <UncompletedTodo />

        </div>
        <div class="todo-completed w-full">
          <h3 class="text-left font-bold text-xl pb-3">COMPLETED</h3>
          <div class="text-center font-bold py-20" v-if="emptyCompletedTodo"> </div>
          <!-- TODO DONE -->
          <CompletedTodo />

        </div>
      </div>

    
</template>

<script>
export default {
  inject: ['emptyTodo', 'emptyCompletedTodo'],
}
</script>