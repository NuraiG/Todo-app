<template>
  <button v-if="!isVisible" class="add" @click="showForm">
    Add a new todo
  </button>
  <button v-if="isVisible" class="add" @click="showForm">
    Hide form
  </button>
  <form v-if="isVisible" @submit.prevent="addTodo" class="todoForm">
    <input type="text" v-model.trim="input" />
    <button class="btn">Add</button>
  </form>
</template>
<script>
import { ref } from "vue";
export default {
  name: "TodoForm",
  emits: ["add"],
  setup(_, context) {
    const newTodo = ref("");
    const isVisible = ref(false);

    function addTodo() {
      if (newTodo.value.trim()) {
        context.emit("add", newTodo.value);
        newTodo.value = "";
      }
      return;
    }
    function showForm() {
      isVisible.value = !isVisible.value;
    }

    return {
      input: newTodo,
      addTodo,
      showForm,
      isVisible,
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
button.btn,
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
button.add {
  padding: 24px;
  border: 3px solid rgb(24, 90, 90);
  background-color: rgb(24, 90, 90);
  border-radius: 6px;
  margin: 20px 100px;
  cursor: pointer;
  color: #fff;
  font-weight: bold;
  outline: none;
  font-size: 1.2rem;
}
button.btn:hover {
  background-color: rgb(24, 90, 90);
  border: 1px solid #fff;
  color: #fff;
}
button.btn {
  width: 100px;
  align-self: flex-end;
}
</style>
