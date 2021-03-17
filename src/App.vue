<template>
  <div id="app">
    <game />
  </div>
</template>

<script>
import Game from "./components/Game";

export default {
  name: "App",
  components: {
    Game,
  },
};
</script>

<style>
body {
  background-color: #2c3e50;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: center;
}
</style>