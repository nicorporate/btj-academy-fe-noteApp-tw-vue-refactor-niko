<template>
  <ul class="flex flex-col gap-5">
    <li class="border-2 rounded-md py-4 px-3 min-h-[117px]" v-for="(todo, index) in todoNotCompleted"
      :key="index">
      <div class="flex flex-col gap-5">
        <h2 class="text-lg font-semibold">{{ todo.name }}</h2>
        <div class="status flex items-center gap-1">
          <span class="w-[10px] h-[10px] block rounded-sm" :class="[
            todo.priority === 'Low'
              ? 'bg-blue-500'
              : todo.priority === 'Medium'
                ? 'bg-orange-500'
                : 'bg-red-600',
          ]"></span>{{ todo.priority }}
        </div>
      </div>
    </li>
  </ul>
</template>

<script>
export default {
  inject: ['todoNotCompleted'],
}
</script>