<template>
  <div
    :class="{
      'form__input-container': true,
      'form__input-container_type_tel': tel
    }"
  >
    <p class="form__input-placeholder">
      {{ placeholder }}
    </p>
    <slot />
    <p
      class="form__input-error"
    >
      {{ isError ? errorMessage || "Поле, обязательное для заполнения" : '' }}
    </p>
  </div>
</template>

<script>
export default {
  name: "InputContainer",
  props: {
    placeholder: {
      type: String,
      default: "Поле"
    },
    isError: {
      type: Boolean,
      default: false
    },
    errorMessage: {
      type: String,
      default: "Поле, обязательное для заполнения"
    },
    tel: {
      type: Boolean,
      default: false
    },
  },
};
</script>

<style scoped  lang="scss">
@import "./InputContainer.sass";
</style>

