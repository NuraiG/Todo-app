<template>
  <my-title :title="userName"></my-title>
  <hr />
  <todo-form @add="addNewItem"></todo-form>
  <todo-list
    :todos="mytodos"
    @removeItem="remove"
    @complete-task="complete"
  ></todo-list>
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
    const userName = "My todo list";
    const defaultData = [
      {
        body: "Learn Vue.js",
        done: false,
      },
    ];
    const todosData = JSON.parse(localStorage.getItem("todos")) || defaultData;
    const todos = ref(todosData);

    function addNewItem(value) {
      todos.value.unshift({ body: value, done: false });
      saveData();
    }
    function removeItem(index) {
      todos.value.splice(index, 1);
      saveData();
    }
    function saveData() {
      const storageData = JSON.stringify(todos.value);
      localStorage.setItem("todos", storageData);
    }
    function completeTask(item) {
      item.done = !item.done;
      saveData();
    }
    return {
      userName,
      addNewItem,
      mytodos: todos,
      remove: removeItem,
      complete: completeTask,
    };
  },
};
</script>

<style>
#app {
  text-align: center;
  font-family: cursive;
  margin: 0 auto;
  padding: 18px;
  width: 40%;
  border: 2px solid rgb(24, 90, 90);
  border-radius: 6px;
  background-color: white;
}
html {
  background: rgb(2, 0, 36);
  background: radial-gradient(
    circle,
    rgba(2, 0, 36, 1) 0%,
    rgba(9, 121, 88, 1) 35%,
    rgba(0, 212, 255, 1) 100%
  );
}
</style>
