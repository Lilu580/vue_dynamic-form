<template>
  <div id="app">
    <DynamicForm />
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import DynamicForm from './components/DynamicForm.vue';

export default defineComponent({
  name: 'App',
  components: {
    DynamicForm
  }
});
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>