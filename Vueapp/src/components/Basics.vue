
<script>
export default {
  mounted() {
    this.$refs.p.textContent = 'Mounted!'
    this.fetchData()
  },
    data() {
        return {
            todoId: 1,
            todoData: null
        }
    },
    methods: {
    async fetchData() {
      this.todoData = null
      const res = await fetch(
        `https://jsonplaceholder.typicode.com/todos/${this.todoId}`
      )
      this.todoData = await res.json()
    }
  },
  watch: {
    todoId() {
      this.fetchData()
    }
  }
}
</script>

<template>
  <p ref="p">The last message to earth</p>
    <p>Todo id: {{ todoId }}</p>
  <button @click="todoId++">Fetch next todo</button>
  <p v-if="!todoData">Loading...</p>
  <pre v-else>{{ todoData }}</pre>
</template>
