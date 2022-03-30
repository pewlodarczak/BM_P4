<script>

let id = 0

export default {
  data() {
    return {
      text: '',
      count: 0,
      awesome: true,
    }
  },
  methods: {
      increment() {
        this.count++
      },
      onInput(e) {
        this.text = e.target.value
    },
    toggle() {
        if(this.awesome)
            this.awesome = false
        else
            this.awesome = true
    },
  }
}</script>

<template>
    <h1>Index</h1>
    <table class="center">
      <tr>
      <td>
    <ul>
      <li><a href="/Basics.html">Basics</a></li>
      <li><a href="/todo.html">ToDo</a></li>
      <li><a href="/newtodo.html">New ToDo</a></li>
      <li><a href="/components.html">Components</a></li>
      <li><a href="/userinput.html">User Input</a></li>
      <li><a href="/congrats.html">Congrats</a></li>
      <li><a href="/edittodo.html">Edit ToDo</a></li>
      <li><a href="/CRUD.html">CRUD</a></li>
      </ul>
    </td>
    </tr>
    </table>
    <br>
    <input :value="text" @input="onInput" placeholder="Type here">
    <p>{{ text }}</p>
    <p><button @click="increment">Count is: {{count}}</button></p>
    <p><button @click="toggle">toggle</button></p>
    <h1 v-if="awesome">This is awesome!</h1>
    <h1 v-else>Oh no 😢</h1>
</template>

<style>
h1 {
  font-family: Arial, Helvetica, sans-serif;
}
body {
  text-align: center;
  background-image: url("/kacktus.jpg");
  background-size: cover;
}
li {
  list-style-position: inside;
  list-style-type: square;
  text-align: left;
}
table.center {
  margin-left: auto; 
  margin-right: auto;
  width: 200px;
  border: 1px solid black;
  font-family: Arial, Helvetica, sans-serif;
}
</style>

