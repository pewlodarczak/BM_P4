<script>
let id = 0;

const STORAGE_KEY = 'vue-todo'

export default {
  data() {
    return {
      newTodo: "",
      hideCompleted: false,
      editedTodo: null,
      /*todos: [],*/
      todos: JSON.parse(localStorage.getItem(STORAGE_KEY) || '[]'),
      visibility: 'all'
    };
  },

  watch: {
    todos: {
      handler(todos) {
        localStorage.setItem(STORAGE_KEY, JSON.stringify(todos))
      },
      deep: true
    }
  },
  computed: {
    filteredTodos() {
      return this.hideCompleted
        ? this.todos.filter((t) => !t.done)
        : this.todos;
    },
        remaining() {
      return filters.active(this.todos).length
    }
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
      console.log('=======>' + todo.text)
      this.beforeEditCache = todo.text
      this.editedTodo = todo
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
    },
    cancelEdit(todo) {
      this.editedTodo = null
      todo.text = this.beforeEditCache
    },
  },
};
</script>

<template>
  <input v-model="newTodo" @keyup.enter="addTodo" autofocus placeholder="What needs to be done?" />
  <button @click="addTodo" >Add Todo</button>
  <br />
  <br />
  <table class="center">
    <tr>
      <th style="text-align: center; width: 300px">ToDo</th>
      <th>Remove</th>
    </tr>
    <tr v-for="todo in filteredTodos" class="todo" :key="todo.id" :class="{ editing: todo === editedTodo }">
      <th style="width: 300px">
        <input type="checkbox" v-model="todo.done" />
        <label @dblclick="editTodo(todo)">{{ todo.text }}</label>
      </th>
      <th style="text-align: center">
        <button @click="removeTodo(todo)">X</button>
      </th>
    </tr>
  </table>
  <br />
      <ul class="todo-list">
        <li
          v-for="todo in filteredTodos"
          class="todo"
          :key="todo.id"
          :class="{ editing: todo === editedTodo }"
       >
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
  <br />
  <button @click="hideCompleted = !hideCompleted">
    {{ hideCompleted ? "Show all" : "Hide completed" }}
  </button>
  <p><button onclick="window.location.href='/index.html'">Home</button></p>

</template>

<style>
/*<@import "https://unpkg.com/todomvc-app-css@2.4.1/index.css";>*/
.done {
  text-decoration: line-through;
}
body {
  text-align: center;
  background-image: url("/kacktus.jpg");
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
ul.todo-list {
  list-style-type: none;
  padding: 0;
  margin: 0;
}
</style>
