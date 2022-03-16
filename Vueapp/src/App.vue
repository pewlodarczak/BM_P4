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
    <p><a href="/Basics.html">Basics</a></p>
    <p><a href="/todo.html">ToDo</a></p>
    <p><a href="/newtodo.html">New ToDo</a></p>
    <p><a href="/components.html">Components</a></p>
    <p><a href="/userinput.html">User Input</a></p>
    <p><a href="/congrats.html">Congrats</a></p>
    <br>
    <input :value="text" @input="onInput" placeholder="Type here">
    <p>{{ text }}</p>
    <p><button @click="increment">Count is: {{count}}</button></p>
    <p><button @click="toggle">toggle</button></p>
    <h1 v-if="awesome">This is awesome!</h1>
    <h1 v-else>Oh no 😢</h1>
</template>

