<template>
    <section id="taskInput">
      <div class="border border-black rounded-sm">
        <div class="flex">
          <!-- FORM TODO -->
          <form class="p-3 flex" action="">
            <div class="flex flex-col mx-2">
              <label for="name">Name</label>
              <input
                v-model="todoInput.name"
                @keyup.enter="addTodo"
                class="bg-white border border-black flex-1 p-2 rounded-l"
                type="text"
              />
            </div>
            <div class="flex flex-col mx-2">
              <label for="priority">Priority</label>
              <select
                v-model="todoInput.priority"
                name="priority"
                id="priority"
                class="p-2 border rounded-r bg-white border-black"
              >
                <option value="High">High</option>
                <option value="Medium">Medium</option>
                <option value="Low">Low</option>
              </select>
            </div>
            <div>
              <button
                class="text-white bg-green-500 py-1"
                type="submit"
                @click="addTodo"
              >
                Save
              </button>
            </div>
          </form>
        </div>
      </div>
    </section>
</template>

<script>
export default {
  inject: ['todoList', 'todoInput', 'addTodo'],
}
</script>