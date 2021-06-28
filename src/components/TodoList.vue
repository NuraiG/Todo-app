<template>
  <div>
    <p v-if="todos.length === 0">I have nothing to do. Yeap, I am free</p>
    <h2 v-else>My todos:</h2>
    <ul>
      <li
        v-for="(todo, index) in todos"
        :key="todo + index"
        @click.stop="done(todo)"
      >
        <span :class="{ done: todo.done }">
          {{ todo.body }}</span
        >
        <button @click.stop="remove(index)">Remove</button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "TodoList",
  props: ["todos"],
  methods: {
    remove(index) {
      this.$emit("removeItem", index);
    },
    done(item) {
      this.$emit("complete-task", item);
    },
  },
};
</script>
<style scoped>
ul {
  margin: 0 auto;
}
li {
  list-style: none;
  text-align: center;
  color: rgb(24, 90, 90);
  font-weight: bold;
  font-size: 1.2rem;
  display: flex;
  justify-content: space-between;
  border: 2px solid rgb(24, 90, 90);
  margin: 5px;
  padding: 6px;
}
button {
  cursor: pointer;
  background-color: rgb(24, 90, 90);
  border: 1px solid #fff;
  color: #fff;
  font-weight: bold;
  outline: none;
  border-radius: 6px;
  padding: 8px;
}
 .done {
  text-decoration: line-through;
}
</style>
