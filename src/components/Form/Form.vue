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

      <Input
        :value="clientData.surname"
        placeholder="Фамилия"
        :is-error="$v.clientData.surname.$error"
        :error-message="errorMessage.surname"
        type="text"
        name="surname"
        maxlength="30"
        :handle-change="handleInputChange"
      />

      <Input
        :value="clientData.name"
        placeholder="Имя"
        :is-error="$v.clientData.name.$error"
        :error-message="errorMessage.name"
        type="text"
        name="name"
        maxlength="30"
        :handle-change="handleInputChange"
      />


      <Input
        :value="clientData.patronymic"
        placeholder="Отчество"
        :is-error="$v.clientData.patronymic.$error"
        :error-message="errorMessage.patronymic"
        type="text"
        name="patronymic"
        maxlength="30"
        :handle-change="handleInputChange"
      />

      <Input
        :value="clientData.dateOfBirth"
        placeholder="Дата рождения"
        :is-error="$v.clientData.dateOfBirth.$error"
        :error-message="errorMessage.dateOfBirth"
        type="date"
        name="dateOfBirth"
        :handle-change="handleInputChange"
      />


      <Input
        :value="clientData.tel"
        placeholder="Номер телефона"
        :is-error="$v.clientData.tel.$error"
        :error-message="errorMessage.tel"
        :tel="true"
        type="tel"
        name="tel"
        maxlength="10"
        :handle-change="handleInputChange"
      />


      <!--В тестовом задании явно не указано какой input использовать, как в у других полей.
          Мне кажется сдесь лучше подойдут radio, например М, Ж, другой-->
      <Input
        :value="clientData.gender"
        placeholder="Пол"
        :is-error="$v.clientData.gender.$error"
        :error-message="errorMessage.gender"
        type="text"
        name="gender"
        maxlength="15"
        :handle-change="handleInputChange"
      />


      <InputContainer
        placeholder="Группа клиентов"
        :is-error="$v.clientData.clientGroup.$error"
        :error-message="constErrorMessage.required"
      >
        <select
          v-model.trim="$v.clientData.clientGroup.$model"
          multiple
          :class="{
            form__select: true,
            form__select_type_multiple: true,
            form__select_error: $v.clientData.clientGroup.$error,
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
      >
        <select
          v-model.trim="$v.clientData.doctor.$model"
          :class="{
            form__select: true,
            form__select_error: $v.clientData.doctor.$error,
          }"
          name="doctor"
        >
          <option>Иванов</option>
          <option>Захаров</option>
          <option>Чернышева</option>
        </select>
      </InputContainer>




      <label class="form__checkbox">
        <input
          v-model.trim="clientData.notSendSms"
          class="form__invisible-checkbox"
          type="checkbox"
          name="notSendSms"
        >
        <span class="form__visible-checkbox" />
        <p class="form__text">Не отправлять СМС</p>
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
import Input from '../Input/Input.vue';
export default {
  name: "Form",
  components: {
    InputContainer,
    Input,
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
        notSendSms: false,
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
      this.actileFieldset++;
    },
    handleInputChange(e) {
      console.log(this.clientData.notSendSms);

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
