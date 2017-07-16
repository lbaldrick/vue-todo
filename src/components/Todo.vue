<template>
  <li class='todo'>
    <section class="todo-details-section" v-show="!isEditing">
      <div class='todo-details-section_title'>
        <span> {{ todo.title }} </span>
      </div>
      <div class='todo-details-section_task'>
        <span> {{ todo.task }} </span>
      </div>
      <div class="todo-details-section_buttons">
        <div class='todo-details-section_buttons_edit'>
          <button class='todo-details-section_buttons_edit_button' v-on:click="showForm">
            Edit
          </button>
        </div>
        <div class='todo-details-section_buttons_delete'>
          <button class='todo-details-section_buttons_delete_button' v-on:click="deleteTodo">
            Delete
          </button>
        </div>
        <div class='todo-details-section_buttons_completed'>
          <button class='todo-details-section_buttons_completed_button' v-show="!isEditing && !todo.completed" v-on:click="completeTodo">
            Completed
          </button>
        </div>
        <div class='todo-details-section_buttons_pending'>
          <button class='todo-details-section_buttons_pending_button' v-show="!isEditing && todo.completed" v-on:click="pendingTodo">
            Pending
          </button>
        </div>
      </div>
    </section>
    <div class="todo-edit-section" v-show="isEditing">
      <div class='todo-edit-section_form'>
        <div class='todo-edit-section_form_field'>
          <label>Title</label>
          <input type='text' v-model="todo.title" >
        </div>
        <div class='todo-edit-section_form_field'>
          <label>Task</label>
          <input type='text' v-model="todo.task" >
        </div>
        <div class='todo-edit-section_form_hide-form'>
          <button class='todo-edit-section-form_hide-form_btn' v-on:click="hideForm">
            Close
          </button>
        </div>
      </div>
    </div>
    <div class='todo-status-completed' v-show="!isEditing && todo.completed">
      Completed
    </div>
    <div class='todo-status-pending' v-show="!isEditing && !todo.completed">
      Pending
    </div>
  </li>
</template>



<script type="text/javascript">
  export default {
    props: [ 'todo', ],
    data () {
      return {
        isEditing: false,
      }
    },
    methods: {
      showForm () {
        this.isEditing = true
      },
      hideForm () {
        this.isEditing = false
      },
      deleteTodo () {
        this.$emit('deleteTodo', this.todo.id)
      },
      completeTodo () {
        this.$emit('completeTodo', this.todo.id)
      },
      pendingTodo () {
        this.$emit('pendingTodo', this.todo.id)
      },
    },
  }
</script>

<style>
  .todo-details-section {
    display: flex;
    padding: 0.5em 0 0 0;
    font-size: 16px;
    font-weight: bold;
  }

  .todo-details-section div {
    padding: 0 0 0 1em;
  }

  .todo-details-section_task {
    width: 75%;
  }

  .todo-details-section_title {
    width: 5%;
  }

  .todo-status-pending,
  .todo-status-completed {
    padding: 0 0 0.5em 0.5em;
    font-size: 17px;
    font-weight: 600;
  }

  .todo-status-pending {
    color: #d08e15;
  }

  .todo-status-completed {
    color: #2f822f;
  }

  .todo-details-section_buttons {
    display: flex;
  }

  .todo-details-section_buttons .todo-details-section_buttons_pending,
  .todo-details-section_buttons .todo-details-section_buttons_completed {
    width: 6em;
    padding: 0 0 0 1em;
  }

  .todo-edit-section_form {
    display: flex;
  }

  .todo-edit-section_form div {
    padding: 0 .5em 0 0;
  }

</style>
