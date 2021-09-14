<template>
  <div id="app">
    <div><strong>使用 单文件组件 形式重新实现此前的项目</strong></div>
    <todo-list>
        <todo-item v-for="item in items" v-bind:key="item.title" @delete="handleDelete" :title="item.title"
            :del="item.del">
            <template v-slot:prefix>
                <span>PREFIX</span>
            </template>
            <template v-slot:suffix="{value}">
                <span>SUFFIX {{value}}</span>
            </template>
        </todo-item>
    </todo-list>
    <hr>
    <div><strong>使用 V-MODEL 实现数据双向绑定</strong></div>
    <div> {{message}} </div>
    <input v-model="message">
    <br><br>
    <div><strong>V-MODEL 的本质是语法糖，负责监听用户的输入以更新数据。它还可以处理以下输入元素：</strong></div>
    <div><strong>text/textarea —— :value @input</strong></div>
    <div><strong>checkbox/radio —— :checked @change</strong></div>
    <div><strong>select —— :value @input</strong></div>
    <input :value="message" @input="handleChange">
    <hr>
    <div><strong>使用 COMPUTED 计算属性</strong></div>
    <div>{{reverseMessage1}}</div>
    <div>{{reverseMessage2()}}</div>
    <button @click="() => $forceUpdate()">Force Update</button>
    <hr>
    <div><strong>使用 WATCH 侦听器</strong></div>
    <div><strong>可以声明 deep 来侦听子元素的数据变化</strong></div>
    <div><strong>作用与 COMPUTED 大致相同，优先使用 COMPUTED </strong></div>
    <div>{{reverseMessage}}</div>
  </div>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
import TodoList from './components/TodoList.vue'
import TodoItem from './components/TodoItem.vue'

export default {
  name: 'App',
  components: {
    // HelloWorld
    TodoList,
    TodoItem
  },
  data() {
    return {
      message: 'Hello Vue!',
      items: [{
                title: 'Course 1',
                del: true
              }, {
                  title: 'Course 2',
                  del: false
              }]
    } 
  },
  computed: {
      reverseMessage1: function() {
          console.log("Update reverseMessage1 using computed");
          return this.message.split("").reverse().join("");
      }
  },
  watch: {
      message: function(val, oldVal) {
          console.log("Detected change! %s -> %s", oldVal, val)
          this.reverseMessage = this.message.split("").reverse().join("");
      }
  },
  methods: {
      handleDelete(val) {
          console.log('Delete item', val)
      },
      handleChange(e) {
          this.message = e.target.value
      },
      reverseMessage2: function() {
          console.log("Update reverseMessage2 using method");
          return this.message.split("").reverse().join("");
      }
  }
}
</script>
