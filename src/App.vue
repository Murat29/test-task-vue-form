<template>
  <div id="app">
    <div class="app">
      <Form />
    </div>
  </div>
</template>

<script>
import Form from './components/Form/Form.vue';

export default {
  name: 'App',
  components: {
    Form,
  },
};
</script>

<style scoped>
.body {
  margin: 0;
}

.app {
  display: flex;
  flex-direction: column;
  align-items: center;
}
</style>
