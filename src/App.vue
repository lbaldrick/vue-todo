<template>
  <div id="app">
    <todo-list v-bind:todos="todos"
               v-on:deleteTodo="deleteTodo"
               v-on:addTodo="addTodo"
               v-on:completeTodo="completeTodo"
               v-on:pendingTodo="pendingTodo"
    >

    </todo-list>
  </div>
</template>

<script>
import TodoList from './components/TodoList'

export default {
  name: 'app',
  components: {
    TodoList,
  },

  methods: {
    deleteTodo (id) {
      this.todos = this.todos.filter((t) => t.id !== id)
    },

    addTodo ({ title, task, }) {
      const todos = this.todos
      const todosLength = todos.length
      const lastTodo = this.todos[todosLength ? todosLength - 1 : todosLength]
      this.todos.push({ id: lastTodo ? 0 : ++lastTodo.id, title, task, completed: false, })
    },

    pendingTodo (id) {
      const todo = this.todos.find((todo) => todo.id === id)
      todo.completed = false
    },

    completeTodo (id) {
      const todo = this.todos.find((todo) => todo.id === id)
      todo.completed = true
    },
  },

  data () {
    return {
      todos: [ {
        id: '1',
        title: '1',
        task: 'Task 1',
        completed: false,
      }, {
        id: '2',
        title: '2',
        task: 'Task 2',
        completed: true,
      }, {
        id: '3',
        title: '3',
        task: 'Task 3',
        completed: false,
      }, {
        id: '4',
        title: '4',
        task: 'Task 4',
        completed: false,
      }, ],
    }
  },
}
</script>

<style>
#app {

}
</style>
