<script>
let id = 0;

const filters = {
  all: (todos) => todos,
  active: (todos) => todos.filter((todo) => !todo.completed),
  completed: (todos) => todos.filter((todo) => todo.completed)
}

export default {
  data() {
    return {
      newTodo: "",
      hideCompleted: false,
      editedTodo: null,
      todos: [],
    };
  },
  computed: {
    filteredTodos() {
      return this.hideCompleted
        ? this.todos.filter((t) => !t.done)
        : this.todos;
    },
    /*
    hideactiveTodos() {
      return this.hideActive
        ? this.todos.filter((t) => t.done)
        : this.todos;
    },*/

  },
  methods: {
    addTodo() {
      this.todos.push({ id: id++, text: this.newTodo });
      this.newTodo = "";
    },
    removeTodo(todo) {
      this.todos = this.todos.filter((t) => t !== todo);
    },
    editTodo(todo) {
      this.beforeEditCache = this.todos.text
      this.editedTodo = this.todos
    },
    doneEdit(todo) {
      if (!this.editedTodo) {
        return
      }
      this.editedTodo = null
      todo.text = todo.text.trim()
      if (!todo.text) {
        this.removeTodo(todo)
      }
    }
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
    <tr v-for="todo in filteredTodos" class="todo" :key="todo.id" :class="{ done: todo.done, editing: todo === editedTodo }">
      <th style="width: 300px">
        <input type="checkbox" v-model="todo.done" />
        <label @dblclick="editTodo(todo)">{{ todo.text }}</label>
        <input
            v-if="todo === editedTodo"
            class="edit"
            type="text"
            v-model="todo.text"
            @vnode-mounted="({ el }) => el.focus()"
            @blur="doneEdit(todo)"
            @keyup.enter="doneEdit(todo)"
            @keyup.escape="cancelEdit(todo)"
          />
        <!--span :class="{ done: todo.done }">{{ todo.text }}</span-->
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

        <ul class="todo-list">
        <li
          v-for="todo in filteredTodos"
          class="todo"
          :key="todo.id"
          :class="{ done: todo.done, editing: todo === editedTodo }"
        >
          <div class="view">
            <input class="toggle" type="checkbox" v-model="todo.done" />
            <label @dblclick="editTodo(todo)">{{ todo.text }}</label>
            <button class="destroy" @click="removeTodo(todo)"></button>
          </div>
          <input
            v-if="todo === editedTodo"
            class="edit"
            type="text"
            v-model="todo.text"
            @vnode-mounted="({ el }) => el.focus()"
            @blur="doneEdit(todo)"
            @keyup.enter="doneEdit(todo)"
            @keyup.escape="cancelEdit(todo)"
          />
        </li>
      </ul>

  <!--button @click="hideActive = !hideActive">
    {{ hideCompleted ? 'Show all' : 'Hide active' }}
  </button-->

  <p><button onclick="window.location.href='/index.html'">Home</button></p>
</template>

<style>
@import "https://unpkg.com/todomvc-app-css@2.4.1/index.css";
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
