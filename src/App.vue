<template>
  <div id="app">
    <h1>Vue 2 TodoList</h1>
    <input v-model="newTodo" @keyup.enter="addTodo" placeholder="Add a new todo" />
    <ul>
      <TodoItem
        v-for="(todo, index) in todos"
        :key="index"
        :todo="todo"
        @remove="removeTodo(todo)"
        @update:completed="updateCompleted(index, $event)"
      />
    </ul>
    <p v-if="todos.length === 0">No more todos!</p>
  </div>
</template>

<script>
import TodoItem from "./components/TodoItem.vue";

export default {
  name: "App",
  components: {
    TodoItem,
  },
  data() {
    return {
      newTodo: "",
      todos:[]
    }
  },
  methods: {
    addTodo() {
      if (this.newTodo.trim() === "") return;
      this.todos.push({ text: this.newTodo.trim(), completed: false})
      this.newTodo = "";
    },
    removeTodo(index) {
      this.todos.splice(index, 1);
    },
    updateCompleted(index, completed) {
      this.$set(this.todos[index], 'completed', completed)
    }
  },
  created() {
    const savedTodos = JSON.parse(localStorage.getItem("todos"));
    if (savedTodos) {
      this.todos = savedTodos;
    }
  },
  watch: {
    todos: {
      handler(newTodos) {
        localStorage.setItem("todos", JSON.stringify(newTodos))
      },
      deep: true // watch change inside the todos array
    }
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: center;
  margin-top: 50px;
}
input {
  padding: 10px;
  width: 300px;
  font-size: 16px;
}
ul {
  list-style: none;
  padding: 0;
}
</style>
