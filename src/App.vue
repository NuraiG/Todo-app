<template>
  <my-title :title="userName"></my-title>
  <hr />
  <todo-form @add="addNewItem"></todo-form>
  <todo-list :todos="mytodos" @removeItem="remove(index)"></todo-list>
</template>

<script>
import MyTitle from "./components/MyTitle.vue";
import TodoForm from "./components/TodoForm.vue";
import TodoList from "./components/TodoList.vue";

import { ref } from "vue";

export default {
  name: "App",
  components: {
    MyTitle,
    TodoForm,
    TodoList,
  },
  setup() {
    const userName = ref("Max");
    const todos = ref([]);

    function addNewItem(value) {
      todos.value.unshift(value);
    }
    function removeItem(index) {
      todos.value.splice(index, 1);
    }
    return {
      userName,
      addNewItem,
      mytodos: todos,
      remove: removeItem,
    };
  },
};
</script>

<style>
#app {
  text-align: center;
  font-family: cursive;
  margin: 0 auto;
  padding: 0;
  width: 60%;
}
</style>
