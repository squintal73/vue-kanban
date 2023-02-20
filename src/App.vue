<template>
  <div class id="app">
    <div class="container grid-xs py-2">
      <img class="img-responsive img-logo" src="@/assets/logo.png" alt="Logomarca da SwitchCase">
      <form @submit.prevent="addTodo(todoW)">
        <div class="input-group">
          <input type="text" v-model="todoW.description" class="form-input" placeholder="Novo todo">
          <button class="btn btn-primary input-group-btn">Adicionar</button>
        </div>
      </form>
      <div class="todo-list">
        <todoW v-for="t in todos" :key="t.id" @toggle="toggleTodo" @remove="removeTodo" :todoW="t"/>
      </div>
    </div>
  </div>
</template>

<script>
import TodoW from "./components/TodoW";

export default {
  name: "app",
  components: { TodoW },
  data() {
    return { todos: [], todoW: { checked: false } };
  },
  methods: {
    addTodo(todoW) {
      todoW.id = Date.now();
      this.todos.push(todoW);
      this.todoW = { checked: false };
    },

    toggleTodo(todoW) {
      const index = this.todos.findIndex(item => item.id === todoW.id);
      if (index > -1) {
        const checked = !this.todos[index].checked;
        this.$set(this.todos, index, { ...this.todos[index], checked });
      }
    },

    removeTodo(todoW) {
      const index = this.todos.findIndex(item => item.id === todoW.id);
      if (index > -1) {
        this.$delete(this.todos, index);
      }
    }
  }
};
</script>

<style scoped>
.img-logo {
  max-width: 200px;
  margin: 0 auto;
}

.todo-list {
  padding-top: 2rem;
}
</style>

