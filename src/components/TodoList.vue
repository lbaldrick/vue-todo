<template>
  <div>
    <div class="todo-list-header"> <span>Completed Tasks: {{todos.filter(todo => todo.completed ).length}} </span> </div>
    <div class="todo-list-header"> <span>Pending Tasks: {{todos.filter(todo => !todo.completed).length}} </span> </div>

    <ul class="todo-list">
      <todo v-for="todo in todos"
            v-bind:todo="todo"
            v-on:deleteTodo="deleteTodo"
            v-on:completeTodo="completeTodo"
            v-on:pendingTodo="pendingTodo"
      >
      </todo>
    </ul>

    <div class="todo-list-add-section" v-show="isAddingTask">
      <div class='todo-list-add-section_form'>
        <div class='todo-list-add-section_form_field'>
          <label>Title</label>
          <input type='text' v-model="newTitle" >
        </div>
        <div class='todo-list-add-section_form_field'>
          <label>Task</label>
          <input type='text' v-model="newTask" >
        </div>
        <div class='todo-list-add-section-form_hide-form'>
          <button class='todo-list-add-section-form_hide-form_btn' v-on:click="toggleAddingTask">
            Close
          </button>
        </div>
        <div class='todo-list-add-section-form_submit-form'>
          <button class='todo-list-add-section-form_submit-form_btn' v-show="isAddingTask" v-on:click="submitForm">
            Submit
          </button>
        </div>
      </div>
    </div>

    <button class="todos-list_add-task-btn" v-show="!isAddingTask" v-on:click="toggleAddingTask">Add Task</button>
  </div>
</template>

<script type = "text/javascript" >

  import Todo from './Todo'

  export default {
    props: [ 'todos', ],
    components: {
      Todo,
    },
    data () {
      return {
        isAddingTask: false,
        newTask: '',
        newTitle: '',
      }
    },
    methods: {
      deleteTodo (id) {
        this.$emit('deleteTodo', id)
      },
      toggleAddingTask () {
        this.isAddingTask = !this.isAddingTask
      },
      submitForm () {
        this.$emit('addTodo', { task: this.newTask, title: this.newTitle, })
        this.toggleAddingTask()
      },
      completeTodo (id) {
        this.$emit('completeTodo', id)
      },
      pendingTodo (id) {
        this.$emit('pendingTodo', id)
      },
    },
  }
</script>

<style>
  .todo-list-header {
    display: flex;
    height: 2em;
    align-items: center;
    justify-content: center;
    background: #5d965d;
    border-top: solid .5em #fff;
    color: #fff;
    font-weight: bold;
    font-size: 18px;
  }
  .todo-list {
    list-style: none;
    padding: 0;
  }

  .todo-list .todo:nth-child(odd) {
    background-color: #daf5da
  }

  .todo-list-add-section_form {
    display: flex;
  }

  .todo-list-add-section_form div {
    padding: 0 .5em 0 0;
  }
</style>

