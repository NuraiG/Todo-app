<template>
  <h3>Add a new todo item</h3>
  <form @submit.prevent="addTodo" class="todoForm">
    <input type="text" v-model.trim="input" />
    <button>Add</button>
  </form>
</template>
<script>
import { ref } from "vue";
export default {
  name: "TodoForm",
  emits: ["add"],
  setup(_, context) {
    const newTodo = ref("");

    function addTodo() {
      if (newTodo.value.trim()) {
        context.emit("add", newTodo.value);
        newTodo.value = "";
      }
      return;
    }

    return {
      input: newTodo,
      addTodo,
    };
  },
};
</script>
<style scoped>
.todoForm {
  display: flex;
  flex-direction: column;
}
input {
  background-color: transparent;
  border: 2px solid gray;
  color: inherit;
}
button,
input {
  height: 48px;
  box-shadow: none;
  outline: none;
  padding-left: 12px;
  padding-right: 12px;
  border-radius: 6px;
  font-size: 18px;
  margin-top: 6px;
  margin-bottom: 12px;
}
h3 {
  padding: 15px;
  border: 3px solid rgb(24, 90, 90);
  background-color: rgb(145 176 171);
  border-radius: 6px;
  margin: 20px 100px;
}
button:hover {
  background-color: rgb(24, 90, 90);
  border: 1px solid #fff;
  color: #fff;
}
button{
  width: 100px;
  align-self: flex-end;

}
</style>
