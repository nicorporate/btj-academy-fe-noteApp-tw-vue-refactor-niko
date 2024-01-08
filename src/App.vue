<script setup>
import ListTodo from "./components/ListTodo.vue";
import { computed } from 'vue'
</script>

<template>
  <div class="container p-5 flex justify-center items-center min-h-screen">
    <ListTodo />
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
  provide() {
    return {
      todoList: this.todoList,
      todoInput: this.todoInput,
      addTodo: this.addTodo,
      deleteTodo: this.deleteTodo,
      completeTodo: this.completeTodo,
      todoCompleted: computed(() => this.todoCompleted),
      todoNotCompleted: computed(() => this.todoNotCompleted),
      todoStatus: computed(() => this.todoStatus),
      emptyCompletedTodo: computed(() => this.emptyCompletedTodo),
      emptyTodo: computed(() => this.emptyTodo)
    }
  },
}
</script>
