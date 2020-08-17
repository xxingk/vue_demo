<template>
  <div>
      <input type="text" class="todo-input" placeholder="needs to be done" v-model="newTodo" @keyup.enter="addTodo">
      <div v-for="(todo, index) in todos" :key="todo.id" class="todo-item">
        <div class="todo-item-left">
          <input type="checkbox" v-model="todo.completed">
          <div class="todo-item-label" v-if="!todo.editing" @dblclick="editTodo(todo)" :class="{completed:todo.completed}">{{todo.title}}</div>
          <input v-else type="text" v-model="todo.title" class="todo-item-edit" @blur="saveTodo(todo)" @keyup.enter="saveTodo(todo)" @keyup.esc="cancelEdit(todo)" v-focus>
        </div>
        <div class="remove-item" @click="removeTodo(index)">&times;</div>
      </div>
      <div class="extra-container">
        <div><label><input type="checkbox" :checked="!anyremaining" @change="checkAllTodos">Check All</label></div>
        <div>{{remaining}} item left</div>
      </div>
  </div>
</template>

<script>
export default {
  name: 'todo-list',
  data () {
    return {
      newTodo: '',
      idForTodo: 3,
      todos: [
        {
          'id':1,
          'title': '学习Vue',
          'complated': false,
          'editing': false,
          'beforeEditCache': '',
          'completed': false
        },
        {
          'id':2,
          'title': '学习Nuxt',
          'complated': false,
          'editing': false,
          'beforeEditCache': '',
          'completed': false
        },
      ],
    }
  },
  directives: {
    //解决多个input同时获得焦点的问题
    focus: {
      inserted: el => {
        el.focus()
      }
    }
  },
  methods: {
    addTodo() {
      if (this.newTodo.trim().length ==0) {
        return
      }
      this.todos.push({
        id: this.idForTodo,
        title: this.newTodo,
        complated: false,
      })

      this.newTodo = ''
      this.idForTodo++
    },

    removeTodo(index) {
      this.todos.splice(index,1)
    },

    editTodo(todo) {
      this.beforeEditCache = todo.title
      todo.editing = true
    },

    saveTodo(todo) {
      if (todo.title.trim() == '') {
        todo.title = this.beforeEditCache
      }
      todo.editing = false
    },

    cancelEdit(todo) {
      todo.title = this.beforeEditCache
      todo.editing = false
    },

    checkAllTodos() {
      this.todos.forEach((todo)=>{
        todo.completed = event.target.checked
      })
    }
  },
  computed: {
    remaining() {
      return this.todos.filter(todo => !todo.completed).length
    },

    anyremaining() {
      return this.remaining != 0
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
    .todo-input {
        width: 100%;
        padding: 10px 18px;
        font-size: 18px;
        margin-bottom: 16px;
    
    }

    .todo-input:focus {
        outline: 0;
    }
    
    .todo-item {
      margin-bottom: 12px;
      display: flex;
      align-items: center;
      justify-content: space-between;
    }

    .remove-item {
      cursor: pointer;
      margin-left: 14px;
    }

    .remove-item:hover {
      color: black;
    }

    .todo-item-left {
      display: flex;
      align-items: center;
    }

    .todo-item-label {
      padding: 10px;
      border: 1px solid white;
      margin-left: 12px;
    }

    .todo-item-edit {
      font-size: 24px;
      color: #2c3e50;
      margin-left: 12px;
      width: 100%;
      padding: 10px;
      border: 1px solid #ccc;
      font-family: Arial, Helvetica, sans-serif;
    }

    .completed {
      text-decoration: line-through;
      color: gray;
    }

    .extra-container {
      display: flex;
      align-items: center;
      justify-content: space-between;
      font-size: 16px;
      border-top: 1px solid lightgray;
      padding-top: 14px;
      margin-bottom: 14px;
    }
    
    button {
      font-size: 14px;
      background-color: white;
      appearance: none;
    }

    button:hover {
      background-color: lightgreen;
    }

    button:focus {
      outline: none;
    }

    .active {
      background-color: lightgreen;
    }
</style>