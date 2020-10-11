<template>
  <li>
    <span v-bind:class="{ done: todo.completed }">
      <input
        v-bind:checked="todo.completed"
        type="checkbox"
        v-on:change="todo.completed = !todo.completed"
      />
      <strong>{{ index + 1 }}.</strong>
      {{ todo.title | uppercase }}
    </span>
    <button class="rm" v-on:click="$emit('remove-todo', todo.id)">
      &times;
    </button>
  </li>
</template>

<script>
export default {
  props: {
    todo: {
      type: Object,
      required: true
    },
    index: Number
  },
  filters: {
    uppercase(value) {
      return value.toUpperCase();
    }
  }
};
</script>

<style lang="scss" scoped>
li {
  border: 1px solid #ccc;
  display: flex;
  justify-content: space-between;
  padding: 14px 20px 5px 20px;
  margin-bottom: 1rem;
  border-radius: 5px;
}

.rm {
  border: 1px solid #ccc;
  border-radius: 3px;
  padding: 3px 6px 0 6px;
  background-color: #fff;
  font-size: 18px;
  margin-bottom: 5px;
  margin-top: -2px;
  &:focus {
    background-color: #ff0000;
    color: #ffffff;
    border-color: #ffffff;
    outline: none;
    box-shadow: none;
  }
}

input {
  margin-right: 20px;
}

.done {
  text-decoration: line-through;
}
</style>
