<script>
export default {
  data() {
    return {
      message: "Hello Brave New World",
      msg: "The last message to earth",
      text: "Edit me",
    };
  },
  methods: {
    reverseMessage() {
      this.message = this.message.split("").reverse().join("");
    },
  },
};
</script>

<template>
  <div class="title">
    <h1>{{ message }}</h1>
    <h2>{{ msg }}</h2>
    <button @click="reverseMessage">Reverse Message</button>
    <h2>Text Input</h2>
    <input v-model="text" /> {{ text }}
  </div>
  <br />
  <button onclick="window.location.href='/index.html'">Home</button>
</template>

<style>
.title {
  font-family: Sans-serif;
  font-weight: bold;
}
h1 {
  color: red;
}
button {
  color: green;
}
body {
  text-align: center;
  background-image: url("/whale.jpg");
  background-size: cover;
  background-color: #e41f1f;
}
</style>