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
    const userName = ref("Max");
    const todos = ref([]);

    function addNewItem(value) {
      todos.value.unshift({ body: value, done: false });
    }
    function removeItem(index) {
      todos.value.splice(index, 1);
    }
    function completeTask(item) {
      item.done = !item.done;
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
  width: 60%;
  border: 2px solid rgb(24, 90, 90);
  border-radius: 6px;
}
</style>
