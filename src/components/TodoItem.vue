<template>
  <li :class="{ completed: todo.completed }">
    <input type="checkbox" :checked="todo.completed" @change="toggleCompleted"> <!-- @是监听事件的缩写-->  <!-- :checked 是v-bind 指令的缩写-->
    <span>{{ todo.text }}</span>
    <button @click="$emit('remove')"> Delete </button>
  </li>
</template>

<script>
export default {
  name: 'TodoItem',
  props: {
    todo: {
      type: Object,
      required: true
    }
  },
  methods: {
    toggleCompleted(event) {
      this.$emit('update:completed', event.target.checked);  // $emit 将子组件中监听的事件传递给父组件，父组件再更新数据，而不是直接更新props
    }
  }
}
</script>

<style scoped>
.completed span {
  text-decoration: line-through;
  color: gray;
}
button {
  margin-left: 10px;
}
</style>