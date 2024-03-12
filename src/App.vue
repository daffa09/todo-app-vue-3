
<template>
  <div>
    <div class="container" style="margin-top: 20px">
      <div class="card">
        <div class="card-body">
          <h5 class="card-title">SIMPLE TODO APP</h5>
          <div class="row">
            <div class="col-10">
              <input v-model="todo" type="text" class="form-control" placeholder="Add a new todo" @keyup.enter="add">
            </div>
            <div class="col-2">
              <button class="btn btn-success" @click="add">Add</button>
            </div>
          </div>
          <List :todos="todos" @deleteTodo="deleteTodo" @doneTodo="doneTodo" @undoneTodo="undDoneTodo"/>
          <br>
          <small>Total Todo : {{ totalTodos }}</small>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import List from './components/List.vue';

export default {
  components: {
    List
  },

  data() {
    return {
      todo: "",
      todos: []
    }
  },

  mounted() {
    this.todos = JSON.parse(localStorage.getItem('todos')) || [];
  },

  computed: {
    totalTodos() {
      return this.todos.length;
    }
  },
  
  methods: {
    add() {
      this.todos.unshift({
        activity: this.todo,
        done: false
      }); //agar yang terbaru paling atas
      this.todo = "";
      this.saveToLocalStorage();
    },

    deleteTodo(todoIndex) {
      this.todos = this.todos.filter((item, index) => {
        if (index != todoIndex) {
          return item;
        }
      })
      this.saveToLocalStorage();
    },

    doneTodo(todoIndex) {
      this.todos = this.todos.filter((item, index) => {
        if (index == todoIndex) {
          item.done = true;
        }

        return item;
      })
      this.saveToLocalStorage();
    },

    undDoneTodo(todoIndex) {
      this.todos = this.todos.filter((item, index) => {
        if (index == todoIndex) {
          item.done = false;
        }

        return item;
      })
      this.saveToLocalStorage();
    },

    saveToLocalStorage() {
      localStorage.setItem('todos', JSON.stringify(this.todos));
    }
  }
}
</script>
