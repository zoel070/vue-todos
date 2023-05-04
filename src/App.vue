<template>
  <div id="app">
    <div class="todoapp">
      <the-header @addTodo="handleAddTodo" />
      <todo-list :todos.sync="todos" :select="select" />
      <the-footer :select.sync="select" :todos.sync="todos" />
    </div>
  </div>
</template>

<script>
import "@/assets/base.css";
import "@/assets/index.css";
import TheHeader from './components/TheHeader.vue';
import TodoList from './components/TodoList.vue';
import TheFooter from './components/TheFooter.vue';


export default {
  name: 'app',
  components: { TheHeader, TodoList, TheFooter, },
  data() {
    return {
      todos: [{
        title: '任务 一',
        completed: false,
      }, {
        title: '任务 二',
        completed: true,
      }, {
        title: '任务 san',
        completed: false,
      },
      {
        title: '任务 si',
        completed: true,
      },
      ],
      select: 'all',
    }
  },
  methods: {
    handleAddTodo(value) {
      this.todos.push({ title: value, completed: false })
    }
  }
}
</script>

<style></style>
