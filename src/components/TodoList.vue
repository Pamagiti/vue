<template>
  <div>
    <ul>
      <TodoItem
        v-for="(todo, i) of todos"
        v-bind:key="todo.id"
        v-bind:index="i"
        v-bind:todo="todo"
        v-on:remove-todo="removeTodo"
      />
    </ul>
  </div>
</template>

<script>
import TodoItem from "@/components/TodoItem";
export default {
  props: ["todos"],
  components: {
    TodoItem
  },
  methods: {
    removeTodo(id) {
      this.$emit("remove-todo", id);
    }
  }
};
</script>

<style lang="scss" scoped>
ul {
  list-style-type: none;
  margin: 0;
  padding: 0;
}</style
>>
