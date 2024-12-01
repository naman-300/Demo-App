<template>
  <div id="app">
    <h1>Basic Quiz App</h1>
    <Quiz />
  </div>
</template>

<script>
import Quiz from './components/Quiz.vue';

export default {
  components: {
    Quiz,
  },
};
</script>

<style>
#app {
  font-family: Arial, sans-serif;
  text-align: center;
  margin: 20px;
}
</style>
