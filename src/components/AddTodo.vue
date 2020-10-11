<template>
  <form @submit.prevent="onSubmit">
    <input type="text" v-model="title" />
    <button class="add" type="submit">+</button>
  </form>
</template>

<script>
export default {
  methods: {
    onSubmit() {
      console.log(this.title);
      if (this.title.trim()) {
        const newTodo = {
          id: Number(new Date()),
          title: this.title,
          completed: false
        };

        this.$emit("add-todo", newTodo);
        this.title = "";
      }
    }
  },
  data() {
    return {
      title: ""
    };
  }
};
</script>
<style lang="scss" scoped>
form {
  display: flex;
  margin: 15px;
  justify-content: center;
}
input {
  width: 400px;
  padding: 10px;
  font-size: 16px;
  border-radius: 5px;
}
.add {
  border-radius: 5px;
  border: none;
  background-color: #fff;
  font-size: 18px;
  margin-left: 20px;
  width: 40px;
  &:focus {
    background-color: #00bb00;
    color: #ffffff;
    outline: none;
    box-shadow: none;
  }
}
</style>
