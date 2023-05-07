<template>
  <div class="container">
    <h1>My Biography</h1>
    <p>My name is Hervé, and I like Nuxt framework based on VueJs.</p>
  </div>
</template>

<script>
export default {
  name: 'AboutPage'
}
</script>

<style>
body {
  border: 8px solid salmon;
  margin: 0;
  height: calc(100vh - 16px);
}
.container {
  font-size: 30px;
  text-align: center;
}
</style>
