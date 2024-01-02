<template>
  <div id="todoapp" class="max-w-md mx-auto">
    <header>
      <h1 class="text-3xl font-bold text-left">TODO APP</h1>
    </header>
    <section id="taskCount" class="flex">
      <div
        class="flex flex-col p-2 border border-black rounded-md m-2"
        v-for="(status, index) in todoStatus"
        :key="index"
      >
        {{ status.name }}
        <div class="font-bold">{{ status.value }}</div>
      </div>
    </section>

    <section id="taskInput">
      <div class="border border-black rounded-sm">
        <div class="flex">
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
              <!-- <input class="bg-white border border-black" type="text" /> -->
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

    <section class="flex mt-2">
      <div class="todos flex flex-wrap justify-between gap-7 lg:gap-3 w-full">
        <div class="todo-not-completed w-full">
          <h3 class="text-left font-bold text-xl pb-3">TODO</h3>
          <ul class="flex flex-col gap-5">
            <div class="text-center font-bold py-20" v-if="emptyTodo"></div>
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
        </div>
        <div class="todo-completed w-full">
          <h3 class="text-left font-bold text-xl pb-3">COMPLETED</h3>
          <div
            class="text-center font-bold py-20"
            v-if="emptyCompletedTodo"
          ></div>
          <ul class="flex flex-col gap-5">
            <li
              class="border border-black rounded-md py-4 px-3"
              v-for="(todo, index) in todoNotCompleted"
              :key="index"
            >
              <div class="flex flex-col gap-5">
                <h2 class="text-lg font-semibold">{{ todo.name }}</h2>
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
              </div>
            </li>
          </ul>
        </div>
      </div>
    </section>
  </div>
</template>

<script>
export default {
  data() {
    return {
      todoList: [],
      todoInput: {
        name: "",
        priority: "",
        isCompleted: false,
      },
    };
  },
  methods: {
    addTodo(e) {
      e.preventDefault();
      if (this.todoInput.name === "") {
        alert("Enter the Task Name");
      } else if (this.todoInput.priority === "") {
        this.todoInput.priority = "Low";
      } else {
        this.todoList.push({
          id: Math.round(Math.random() * (1 - 100)),
          name: this.todoInput.name,
          priority: this.todoInput.priority,
          isCompleted: false,
        });
        this.todoInput.name = "";
        this.todoInput.priority = "";
      }
    },
    deleteTodo(id) {
      this.todoList = this.todoList.filter((todo) => todo.id !== id);
    },
    completeTodo(id) {
      this.todoList.map((todo) => {
        if (id === todo.id) {
          todo.isCompleted = !todo.isCompleted;
        }
      });
    },
  },
  computed: {
    todoCompleted() {
      return this.todoList.filter((todo) => !todo.isCompleted);
    },
    todoNotCompleted() {
      return this.todoList.filter((todo) => todo.isCompleted);
    },
    pendingTodo() {
      let pending = this.todoList.filter((todo) => !todo.isCompleted);
      return pending.length;
    },
    lowPriorityTodo() {
      let lowPriority = this.todoList.filter(
        (todo) => todo.priority === "Low" && !todo.isCompleted
      );
      return lowPriority.length;
    },
    mediumPriorityTodo() {
      let mediumPriority = this.todoList.filter(
        (todo) => todo.priority === "Medium" && !todo.isCompleted
      );
      return mediumPriority.length;
    },
    highPriorityTodo() {
      let highPriority = this.todoList.filter(
        (todo) => todo.priority === "High" && !todo.isCompleted
      );
      return highPriority.length;
    },
    
    todoStatus() {
      return [
        {
          name: "PENDING",
          value: this.pendingTodo,
        },
        {
          name: "LOW",
          value: this.lowPriorityTodo,
        },
        {
          name: "MEDIUM",
          value: this.mediumPriorityTodo,
        },
        {
          name: "HIGH",
          value: this.highPriorityTodo,
        },
      ];
    },
    emptyTodo() {
      return this.todoCompleted.length === 0;
    },
    emptyCompletedTodo() {
      return this.todoNotCompleted.length === 0;
    },
  },
};
</script>
