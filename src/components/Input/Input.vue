<template>
  <InputContainer
    :placeholder="placeholder"
    :is-error="isError"
    :error-message="errorMessage"
    :tel="tel"
  >
    <input
      :value="value"
      :class="{
        form__input: true,
        form__input_error: isError,
        form__input_type_tel: tel,
      }"
      :type="type"
      :name="name"
      :maxlength="maxlength"
      @input="handleChange($event)"
    >
  </InputContainer>
</template>

<script>
import InputContainer from '../InputContainer/InputContainer.vue';

export default {
  name: "Input",
  components: {
    InputContainer,
  },
  props: {
    placeholder: {
      type: String,
      default: "Поле",
    },
    isError: {
      type: Boolean,
      default: false,
    },
    errorMessage: {
      type: String,
      default: "",
    },
    tel: {
      type: Boolean,
      default: false,
    },
    type: {
      type: String,
      default: 'text',
    },
    name: {
      type: String,
      default: '',
    },
    maxlength: {
      type: String,
      default: '30',
    },
    handleChange: {
      type: Function,
      default: ()=>{},
    },
    value: {
      type: String,
      default: "",
    },
  },
};
</script>

<style scoped  lang="scss">
@import "./Input.sass";
</style>

