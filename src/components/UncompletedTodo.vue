<template>
          <ul class="flex flex-col gap-5">
            <li
              class="border border-black rounded-md py-4 px-3"
              v-for="(todo, index) in todoCompleted"
              :key="index"
            >
              <div class="flex flex-col gap-5">
                <h2 class="text-lg font-semibold">{{ todo.name }}</h2>
                <div class="flex items-center justify-between">
                  <div class="status flex items-center gap-1">
                    <span
                      class="w-[10px] h-[10px] block rounded-sm"
                      :class="[
                        todo.priority === 'Low'
                          ? 'bg-blue-500'
                          : todo.priority === 'Medium'
                          ? 'bg-orange-500'
                          : 'bg-red-600',
                      ]"
                    ></span
                    >{{ todo.priority }}
                  </div>
                  <div class="action-button flex gap-2 items-center">
                    <button
                      @click="deleteTodo(todo.id)"
                      class="py-1 px-4 bg-red-500 rounded-md text-white"
                    >
                      Delete
                    </button>
                    <button
                      @click="completeTodo(todo.id)"
                      class="py-1 px-4 bg-green-500 rounded-md text-white"
                    >
                      Complete
                    </button>
                  </div>
                </div>
              </div>
            </li>
          </ul>
</template>

<script>
export default {
  inject: ['todoCompleted', 'deleteTodo', 'completeTodo'],
}
</script>