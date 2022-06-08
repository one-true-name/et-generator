<template>
  <img alt="Dftba logo" src="./assets/dftba.svg" height="200">
  <vETGenerator />
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import vETGenerator from './components/vETGenerator.vue';

export default defineComponent({
  name: 'App',
  components: {
    vETGenerator
  }
});
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
