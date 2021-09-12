<template>
  <header>
    <section>
      <label for="title">ToDoList</label>
      <input
        type="text"
        name="title"
        placeholder="添加ToDo"
        required="required"
        autocomplete="off"
        v-model="inputContent"
        @keydown.enter="submit"
      />
    </section>
  </header>
</template>

<script>
export default {
  name: 'Header',
  data() {
    return {
      inputContent: ''
    }
  },
  methods: {
    submit() {
      this.$emit('submit', this.inputContent)
      this.inputContent = ''
    }
  }
}
</script>

<style scoped>
header {
  height: 50px;
  background: #333;
  background: rgba(47, 47, 47, 0.98);
}

label {
  float: left;
  width: 100px;
  line-height: 50px;
  color: #ddd;
  font-size: 24px;
  cursor: pointer;
  font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif;
}

header input {
  float: right;
  width: 60%;
  height: 24px;
  margin-top: 12px;
  text-indent: 10px;
  border-radius: 5px;
  box-shadow: 0 1px 0 rgba(255, 255, 255, 0.24), 0 1px 6px rgba(0, 0, 0, 0.45) inset;
  border: none;
}

input:focus {
  outline-width: 0;
}
</style>
