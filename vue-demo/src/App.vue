<template>
  <div id="app">
    <mark>使用 slot 来定义插槽，分类：默认插槽、具名插槽、作用域插槽</mark><br>
    <mark>默认插槽：组件嵌套中实际上就是使用了子组件的 template 作为默认插槽</mark><br>
    <mark>具名插槽：带有名称的 template </mark><br>
    <mark>作用域插槽：可以接收子组件传递的值 </mark><br>
    <mark>定义的插槽未在模板中使用时，将使用默认值，尝试删除第二个 template 查看效果</mark><br>
    <todo-list>
        <todo-item v-for="item in items" v-bind:key="item.title" @delete="handleDelete" :title="item.title"
            :del="item.del">
            <!-- SLOT SYNTAX - Vue 2.5 and earlier
            <span slot="prefix">PREFIX</span>
            <span slot="suffix">SUFFIX</span>
            -->
            <!-- SLOT SYNTAX - Vue 2.6+ -->
            <template v-slot:prefix>
                <span>PREFIX</span>
            </template>
            <template v-slot:suffix="{value}">
                <span>SUFFIX {{value}}</span>
            </template>
        </todo-item>
    </todo-list>
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
      items: [{
                title: 'Course 1',
                del: true
              }, {
                  title: 'Course 2',
                  del: false
              }]
    } 
  },
  methods: {
      handleDelete(val) {
          console.log('Delete item', val)
      }
  }
}
</script>
