<template>
  <h1>{{ title }} </h1>
</template>

<script>
export default {
  name: "MyTitle",
  props: {
    title: {
      type: String,
      required: true,
    },
  },
};
</script>

<style>
h1{
  color: rgb(24, 90, 90);
}
</style>
