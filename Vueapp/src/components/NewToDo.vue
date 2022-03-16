<script>
let id = 0;

export default {
  data() {
    return {
      newTodo: "",
      hideCompleted: false,
      todos: [],
    };
  },
  computed: {
    filteredTodos() {
      return this.hideCompleted
        ? this.todos.filter((t) => !t.done)
        : this.todos;
    },
  },
  methods: {
    addTodo() {
      this.todos.push({ id: id++, text: this.newTodo });
      this.newTodo = "";
    },
    removeTodo(todo) {
      this.todos = this.todos.filter((t) => t !== todo);
    },
  },
};
</script>

<template>
  <input v-model="newTodo" @keyup.enter="addTodo" />
  <button @click="addTodo">Add Todo</button>
  <br />
  <br />
  <table class="center">
    <tr>
      <th style="text-align: center; width: 300px">ToDo</th>
      <th>Remove</th>
    </tr>
    <tr v-for="todo in filteredTodos" :key="todo.id">
      <th style="width: 300px">
        <input type="checkbox" v-model="todo.done" />
        <span :class="{ done: todo.done }">{{ todo.text }}</span>
      </th>
      <th style="text-align: center">
        <button @click="removeTodo(todo)">X</button>
      </th>
    </tr>
  </table>
  <br />
  <button @click="hideCompleted = !hideCompleted">
    {{ hideCompleted ? "Show all" : "Hide completed" }}
  </button>
  <!--p><a href="/index.html">Take me home</a></p-->
  <p><button onclick="window.location.href='/index.html'">Home</button></p>
</template>

<style>
.done {
  text-decoration: line-through;
}
body {
  text-align: center;
  background-image: url("/wires.jpg");
  background-size: cover;
}
table,
tr,
th {
  text-align: left;
  font-family: Sans-serif;
  border: 1px solid black;
}
.center {
  margin-left: auto;
  margin-right: auto;
}
</style>
