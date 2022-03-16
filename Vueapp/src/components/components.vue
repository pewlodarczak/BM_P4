
<script>
import ChildComp from './ChildComp.vue'

export default {
  components: {
    ChildComp
  },
   data() {
    return {
      greeting: 'Hello from parent',
      childMsg: 'No child msg yet',
      msg: 'Slot message'
    }
  }
}
</script>

<template>
  <!--ChildComp :msg="greeting" /-->
  <ChildComp :msg="greeting" @response="(msg) => childMsg = msg">
  Message: {{msg}}
</ChildComp>
<div class="childmsg">
  <p>{{ childMsg }}</p>
</div>
</template>

<style>
.childmsg {
  font-family: Sans-serif;
  font-weight: bold;
}
</style>