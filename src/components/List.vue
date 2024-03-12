<template>
  <div style="margin-top: 20px">
    <ul class="list-group">
      <li class="list-group-item" v-for="(todo, index) in todos" :key="index">
        <div class="row">
          <div class="col">
            <span v-if="todo.done">
              <del>{{ todo.activity }}</del>
            </span>
          <span v-else>{{ todo.activity }}</span>
          </div>
          <div class="col-auto">
            <div class="row gx-2">
              <div class="col">
                <button @click="done(index)" class="btn btn-info" v-if="!todo.done">Done</button>
                <button @click="udDone(index)" class="btn btn-primary" v-else>UnDone</button>
              </div>
              <div class="col">
                <button @click="deleteTodo(index)" class="btn btn-danger">X</button>
              </div>
            </div>
          </div>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  props: {
    todos:{
      type: Array,
      default: []
    }
  },

  methods: {
    deleteTodo(index) {
      this.$emit('deleteTodo', index);
    },

    done(index){
      this.$emit('doneTodo', index);
    },

    udDone(index){
      this.$emit('undoneTodo', index);
    }
  }
}
</script>
