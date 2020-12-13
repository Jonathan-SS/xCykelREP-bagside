<template>
  <div id="app">
    <contact-posts></contact-posts>
  </div>
</template>

<script>
import ContactPosts from "./components/contactPosts.vue"; export default { name:
"App", components: { ContactPosts } };
</script>

<style>
body {
  background-color: #3a393e;
  color: azure;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: left;
  background-color: #3a393e;
}
h1 {
  font-family: Tahoma, Geneva, Verdana, sans-serif;
}
</style>
