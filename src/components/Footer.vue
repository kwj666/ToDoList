<template>
  <footer>
    Copyright &copy; 2021 ToDoList made by Vue <button @click="clearData">clear</button>
  </footer>
</template>

<script>
export default {
  name: 'Footer',
  props: ['toDoList'],
  methods: {
    clearData() {
      this.$emit('clearData', [])
    }
  }
}
</script>

<style scoped>
footer {
  color: #666;
  font-size: 14px;
  text-align: center;
}

footer button {
  display: inline-block;
  border-radius: 5px;
  outline: none;
  border: none;
  background-color: #333;
  color: #fff;
  text-decoration: none;
  cursor: pointer;
}
</style>
