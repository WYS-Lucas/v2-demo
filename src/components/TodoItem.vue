<template>
  <li :class="{ completed: todo.completed }">
    <input type="checkbox" :checked="todo.completed" @change="toggleCompleted">
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
      this.$emit('update:completed', event.target.checked);
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