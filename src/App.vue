<template>
  <div id="app">
    <!-- 底部区域 -->
    <Header @submit="submit"></Header>
    <!-- 内容区域 -->
    <Content
      :doingNum="doingNum"
      :doneNum="doneNum"
      :doingToDoList="doingToDoList"
      :doneToDoList="doneToDoList"
      @deleteData="deleteData"
    ></Content>
    <!-- 底部版权 -->
    <Footer :toDoList="toDoList" @clearData="clearData"></Footer>
  </div>
</template>

<script>
import Footer from './components/Footer.vue'
import Header from './components/Header.vue'
import Content from './components/Content.vue'
export default {
  name: 'App',
  components: {
    Footer,
    Header,
    Content
  },
  data() {
    return {
      // 输入框内容
      inputContent: '',
      // 用来存放todo所有的内容
      toDoList: []
    }
  },
  // 加载页面时获取本地存储数据
  created() {
    this.toDoList = this.getData()
  },
  // 数据发生更新时将新数据保存到本地存储
  updated() {
    this.saveData(this.toDoList)
  },
  computed: {
    // 正在进行的数据
    doingToDoList() {
      return this.toDoList.filter(item => !item.done)
    },
    // 已经完成的数据
    doneToDoList() {
      return this.toDoList.filter(item => item.done)
    },
    // 正在进行的数量
    doingNum() {
      let doingTodoList = this.toDoList.filter(item => !item.done)
      return doingTodoList.length
    },
    // 已经完成的数量
    doneNum() {
      let doingTodoList = this.toDoList.filter(item => item.done)
      return doingTodoList.length
    }
  },

  methods: {
    // 文本框中回车保存数据
    submit(val) {
      this.inputContent = val
      if (!this.inputContent) return alert('你没有填写任何内容哦！')
      let toDoObj = {
        // 时间戳作为id
        id: +new Date(),
        title: this.inputContent,
        done: false
      }
      this.toDoList.unshift(toDoObj)
      this.inputContent = ''
      this.saveData(this.toDoList)
    },

    // 删除按钮事件
    deleteData(id) {
      let data = this.getData()
      let newToDoList = data.filter(item => {
        return item.id != id
      })
      // 删除后将新数据保存到本地存储
      this.saveData(newToDoList)
      this.toDoList = newToDoList
    },
    // 清除按钮事件
    clearData(data) {
      this.toDoList = data
    },
    // 将数据保存到本地存储
    saveData(data) {
      localStorage.setItem('todolist', JSON.stringify(data))
    },
    // 获取本地存储的数据
    getData() {
      let data = localStorage.getItem('todolist')
      if (data != null) {
        // 本地存储的数据是字符串类型 我们需要转换为对象格式
        return JSON.parse(data)
      } else {
        return []
      }
    }
  }
}
</script>

<style></style>
