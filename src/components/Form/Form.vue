<template>
  <form class="form">
    <h1 class="form__title">
      Регистрация
    </h1>
    <fieldset class="form__fieldset">
      <legend>Личные данные</legend>
      <input
        type="text"
        placeholder="Фамилия"
        required
      >
      <input
        type="text"
        placeholder="Имя"
        required
      >
      <input
        type="text"
        placeholder="Отчество"
      >
      <input
        type="date"
        placeholder="Дата рождения"
        required
      >
      <input
        type="tel"
        placeholder="Номер телефона"
        required
      >
      <input
        type="text"
        placeholder="Пол"
      >
      <select multiple>
        <option>VIP</option>
        <option>Проблемные</option>
        <option>ОМС</option>
      </select>
      <select>
        <option>Иванов</option>
        <option>Захаров</option>
        <option>Чернышева</option>
      </select>
      <input
        type="checkbox"
        placeholder="Не отправлять СМС"
      >
    </fieldset>
    <fieldset class="form__fieldset">
      <legend>Адрес</legend>
      <input
        type="number"
        placeholder="Индекс"
      >
      <input
        type="text"
        placeholder="Страна"
      >
      <input
        type="text"
        placeholder="Область"
      >
      <input
        type="text"
        placeholder="Город"
        required
      >
      <input
        type="text"
        placeholder="Улица"
      >
      <input
        type="text"
        placeholder="Дом"
        required
      >
    </fieldset>
    <fieldset class="form__fieldset">
      <legend>Паспорт</legend>
      <select>
        <option>Паспорт</option>
        <option>Свидетельство о рождении</option>
        <option>Вод. удостоверение</option>
      </select>
      <input
        type="number"
        placeholder="Серия"
      >
      <input
        type="number"
        placeholder="Номер"
      >
      <input
        type="text"
        placeholder="Кем выдан"
      >
      <input
        type="date"
        placeholder="Дата выдачи"
        required
      >
    </fieldset>
  </form>
</template>

<style scoped lang="scss">
@import "./Form.sass";
</style>

<script>
export default {
  data() {
    return {
      title: 'Привfdgdfgет мир!',
    };
  },
};
</script>
