<template>
  <div id="app">
    <div class="app">
      <Form />
    </div>
  </div>
</template>

<script>
import Form from '../Form/Form.vue';

export default {
  name: 'App',
  components: {
    Form,
  },
};
</script>

<style  lang="css">
@import "../vendor/InterWeb/inter.css";
html, body {
  margin: 0px !important;
  padding: 0px !important;
}
</style>

<style  lang="scss">
@import "./App.sass";
</style>

