<template>
  <div>
    <h2>To do app by Android-HA</h2>
    <router-link to="/">Home</router-link>
    <hr />

    <AddTodo @add-todo="addTodo" />
    <select v-model="filter">
      <option value="all">All</option>
      <option value="completed">Completed</option>
      <option value="not-completed">Not completed</option>
    </select>

    <Loader v-if="loading" />
    <TodoList
      v-bind:todos="filteredTodos"
      @remove-todo="removeTodo"
      v-else-if="filteredTodos.length"
    />
    <p v-else>No todos</p>
  </div>
</template>

<script lang="ts">
import TodoList from "@/components/TodoList.vue";
import AddTodo from "@/components/AddTodo.vue";
import Loader from "@/components/Loader.vue";

export default {
  name: "App",
  data() {
    return {
      todos: [],
      loading: true,
      filter: "all"
    };
  },
  mounted() {
    fetch("https://jsonplaceholder.typicode.com/todos?_limit=5")
      .then(response => response.json())
      .then(json => {
        setTimeout(() => {
          this.todos = json;
          this.loading = false;
        }, 2000);
      });
  },
  components: {
    TodoList,
    AddTodo,
    Loader
  },
  // watch: {
  //   filter(value) {
  //     console.log(value);

  //   }
  // },
  methods: {
    removeTodo(id: number) {
      this.todos = this.todos.filter((t: any) => t.id !== id);
    },
    addTodo(todo: any) {
      this.todos.push(todo);
    }
  },
  computed: {
    filteredTodos() {
      if (this.filter === "all") {
        return this.todos;
      }

      if (this.filter === "completed") {
        return this.todos.filter(t => t.completed);
      }

      if (this.filter === "not-completed") {
        return this.todos.filter(t => !t.completed);
      }

      return null;
    }
  }
};
</script>

<style lang="scss" stoped>
select {
  padding: 5px;
  margin: 5px 5px 20px 5px;
}
</style>
