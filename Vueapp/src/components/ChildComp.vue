
<script>
export default {
    emits: ['response'],
    created() {
    this.$emit('response', 'hello from child')
  },
  props: {
    msg: String
  }
}
</script>

<template>
  <div class="title">
    <h1>A Child Component</h1>
  <h2>{{ msg || 'No props passed yet' }}</h2>
  </div>
  <div class="slot">
    <slot>Fallback content</slot>
  </div>
</template>

<style>
.title {
  font-family: Sans-serif;
}
.slot {
  font-family: Sans-serif;
  font-weight: bold;
}
</style>
