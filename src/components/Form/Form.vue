<template>
  <form
    class="form"
    novalidate
  >
    <h1 class="form__title">
      Регистрация
    </h1>
    <div class="form__promotion">
      <div
        :class="{
          form__dot: true,
          form__dot__finish: actileFieldset > 1,
          form__dot__active: actileFieldset === 1,
        }"
      />
      <div
        :class="{
          form__dot: true,
          form__dot__finish: actileFieldset > 2,
          form__dot__active: actileFieldset === 2,
        }"
      />
      <div
        :class="{
          form__dot: true,
          form__dot__finish: actileFieldset > 3,
          form__dot__active: actileFieldset === 3,
        }"
      />
    </div>
    <fieldset
      v-show="actileFieldset === 1"
      class="form__fieldset"
    >
      <legend class="form__legend">
        Личные данные
      </legend>

      <InputContainer
        placeholder="Фамилия"
        :is-error="$v.clientData.surname.$error"
        :error-message="errorMessage.surname"
      >
        <input
          v-model.trim="clientData.surname"
          :class="{
            form__input_error: $v.clientData.surname.$error,
            form__input: true,
          }"
          type="text"
          name="surname"
          maxlength="30"
          @input="handleInputChange($event)"
        >
      </InputContainer>

      <InputContainer
        placeholder="Имя"
        :is-error="$v.clientData.name.$error"
        :error-message="errorMessage.name"
      >
        <input
          v-model.trim="clientData.name"
          :class="{
            form__input_error: $v.clientData.name.$error,
            form__input: true,
          }"
          type="text"
          name="name"
          maxlength="30"
          @input="handleInputChange($event)"
        >
      </InputContainer>

      <InputContainer
        placeholder="Отчество"
        :is-error="$v.clientData.patronymic.$error"
        :error-message="errorMessage.patronymic"
      >
        <input
          v-model.trim="clientData.patronymic"
          :class="{
            form__input_error: $v.clientData.patronymic.$error,
            form__input: true,
          }"
          type="text"
          name="patronymic"
          maxlength="30"
          @input="handleInputChange($event)"
        >
      </InputContainer>

      <InputContainer
        placeholder="Дата рождения"
        :is-error="$v.clientData.dateOfBirth.$error"
        :error-message="errorMessage.dateOfBirth"
      >
        <input
          v-model.trim="clientData.dateOfBirth"
          :class="{
            form__input_error: $v.clientData.dateOfBirth.$error,
            form__input: true,
          }"
          type="date"
          name="dateOfBirth"
          @input="handleInputChange($event)"
        >
      </InputContainer>

      <InputContainer
        placeholder="Номер телефона"
        :is-error="$v.clientData.tel.$error"
        :error-message="errorMessage.tel"
        :tel="true"
      >
        <input
          v-model.trim="clientData.tel"
          :class="{
            form__input_error: $v.clientData.tel.$error,
            form__input: true,
            form__input_tel: true,
          }"
          type="tel"
          name="tel"
          maxlength="10"
          @input="handleInputChange($event)"
        >
      </InputContainer>

      <!--В тестовом задании явно не указано какой input использовать, как в у других полей.
          Мне кажется сдесь лучше подойдут radio, например М, Ж, другой-->
      <InputContainer
        placeholder="Пол"
        :is-error="$v.clientData.gender.$error"
        :error-message="errorMessage.gender"
      >
        <input
          v-model.trim="clientData.gender"
          :class="{
            form__input_error: $v.clientData.gender.$error,
            form__input: true,
          }"
          type="text"
          name="gender"
          maxlength="15"
          @input="handleInputChange($event)"
        >
      </InputContainer>

      <InputContainer
        placeholder="Группа клиентов"
        :is-error="$v.clientData.clientGroup.$error"
        :error-message="constErrorMessage.required"
      >
        <select
          v-model.trim="$v.clientData.clientGroup.$model"
          multiple
          :class="{
            form__input: true,
            form__input_type_multiple: true,
            form__input_error: $v.clientData.clientGroup.$error,
          }"
          name="clientGroup"
        >
          <option>VIP</option>
          <option>Проблемные</option>
          <option>ОМС</option>
        </select>
      </InputContainer>

      <InputContainer
        placeholder="Лечащий врач"
        :is-error="$v.clientData.doctor.$error"
        :error-message="''"
      >
        <select
          v-model.trim="$v.clientData.doctor.$model"
          :class="{
            form__input: true,
            form__input_error: $v.clientData.doctor.$error,
          }"
          name="doctor"
        >
          <option>Иванов</option>
          <option>Захаров</option>
          <option>Чернышева</option>
        </select>
      </InputContainer>




      <label class="filter-checkbox">
        <input

          id="filter-shortfilm"
          class="filter-checkbox__invisible-checkbox"
          type="checkbox"
          name="shortfilm"
        >
        <span class="filter-checkbox__visible-checkbox" />
        <p class="filter-checkbox__text">Не отправлять СМС</p>
      </label>
    </fieldset>
    <fieldset
      v-show="actileFieldset === 2"
      class="form__fieldset"
    >
      <legend class="form__legend">
        Адрес
      </legend>
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
    <fieldset
      v-show="actileFieldset === 3"
      class="form__fieldset"
    >
      <legend class="form__legend">
        Паспорт
      </legend>
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
    <button
      class="form__submit"
      @click="submit"
    >
      Далее
    </button>
  </form>
</template>


<script>
import { required, minLength, numeric } from "vuelidate/lib/validators";
import InputContainer from '../InputContainer/InputContainer.vue';
export default {
  name: "Form",
  components: {
    InputContainer,
  },
  data() {
    return {
      actileFieldset: 1,
      clientData: {
        surname: null,
        name: null,
        patronymic: null,
        dateOfBirth: null,
        tel: null,
        gender: null,
        clientGroup: [],
        doctor: null,
      },
      errorMessage: {
        surname: '',
        name: '',
        patronymic: '',
        dateOfBirth: '',
        tel: '',
        gender: '',
        clientGroup: '',
        doctor: '',
      },
      constErrorMessage: {
        required: "Поле, обязательное для заполнения",
      },
    };
  },

   validations: {
        clientData: {
        surname: {
          required,
          minLength: minLength(2),
        },
        name: {
          required,
          minLength: minLength(2),
        },
        patronymic: {
          minLength: minLength(2),
        },
        dateOfBirth: {
          required,
        },
        tel: {
          required,
          numeric,
          minLength: minLength(10),
        },
        gender: {},
        clientGroup: {
          required,
        },
        doctor: {},
      },
  },

  methods: {
    submit(e) {
      e.preventDefault();
      console.log($v.name);
      this.actileFieldset++;
    },
    handleInputChange(e) {
      console.log(this.clientData.doctor);
      // обновление данных
      const name = e.target.name;
      this.clientData[name] = e.target.value;
      this.$v.clientData[name].$touch();

      // обновление собщения об ошибке
      if (!this.$v.clientData[name].$error) {
        this.errorMessage[name] = ''
        return ;
      } else {
          if (this.$v.clientData[name].required !== undefined && !this.$v.clientData[name].required){
            this.errorMessage[name] =  this.constErrorMessage.required;
            return;
            } else if (this.$v.clientData[name].numeric !== undefined && !this.$v.clientData[name].numeric) {
            this.errorMessage[name] = 'Поле должно содержать не менее только цифры';
            return
            } else if (this.$v.clientData[name].minLength !== undefined && !this.$v.clientData[name].minLength) {
            this.errorMessage[name] = `Поле должно содержать не менее ${this.$v.clientData[name].$params.minLength.min } символов`;
            return
            }
          this.errorMessage[name] ='Не допустимое значение';
          return;
        }

    },
  }
};
</script>

<style scoped lang="scss">
@import "./Form.sass";
</style>
