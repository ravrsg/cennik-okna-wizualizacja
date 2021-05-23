<template>
  <v-app>
    <v-main>
      <v-container fluid>
        <main-comp></main-comp>
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
import mainCopmonent from "./components/mainComponent";
export default {
  name: "App",
  components: {
    "main-comp": mainCopmonent,
  },
};
</script>

<style>
MainComponent #app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
