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
        v-for="(el, i) in arrayFieldset"
        :key="el"
        :class="{
          form__dot: true,
          form__dot__finish: actileFieldset > i,
          form__dot__active: actileFieldset === i,
        }"
      />
    </div>
    <fieldset
      v-show="actileFieldset === 0"
      class="form__fieldset"
    >
      <legend class="form__legend">
        Личные данные
      </legend>

      <Input
        :value="clientData.personalData.surname"
        placeholder="Фамилия"
        :is-error="$v.clientData.personalData.surname.$error"
        :error-message="errorMessage.personalData.surname"
        type="text"
        group-name="personalData"
        name="surname"
        maxlength="30"
        :handle-change="handleInputChange"
      />

      <Input
        :value="clientData.personalData.name"
        placeholder="Имя"
        :is-error="$v.clientData.personalData.name.$error"
        :error-message="errorMessage.personalData.name"
        type="text"
        group-name="personalData"
        name="name"
        maxlength="30"
        :handle-change="handleInputChange"
      />


      <Input
        :value="clientData.personalData.patronymic"
        placeholder="Отчество"
        :is-error="$v.clientData.personalData.patronymic.$error"
        :error-message="errorMessage.personalData.patronymic"
        type="text"
        group-name="personalData"
        name="patronymic"
        maxlength="30"
        :handle-change="handleInputChange"
      />

      <Input
        :value="clientData.personalData.dateOfBirth"
        placeholder="Дата рождения"
        :is-error="$v.clientData.personalData.dateOfBirth.$error"
        :error-message="errorMessage.personalData.dateOfBirth"
        type="date"
        group-name="personalData"
        name="dateOfBirth"
        :handle-change="handleInputChange"
      />


      <Input
        :value="clientData.personalData.tel"
        placeholder="Номер телефона"
        :is-error="$v.clientData.personalData.tel.$error"
        :error-message="errorMessage.personalData.tel"
        :tel="true"
        type="tel"
        group-name="personalData"
        name="tel"
        maxlength="10"
        :handle-change="handleInputChange"
      />


      <!--В тестовом задании явно не указано какой input использовать, как в у других полей.
          Мне кажется сдесь лучше подойдут radio, например М, Ж, другой-->
      <Input
        :value="clientData.personalData.gender"
        placeholder="Пол"
        :is-error="$v.clientData.personalData.gender.$error"
        :error-message="errorMessage.personalData.gender"
        type="text"
        group-name="personalData"
        name="gender"
        maxlength="15"
        :handle-change="handleInputChange"
      />


      <InputContainer
        placeholder="Группа клиентов"
        :is-error="$v.clientData.personalData.clientGroup.$error"
        :error-message="constErrorMessage.required"
      >
        <select
          v-model.trim="$v.clientData.personalData.clientGroup.$model"
          multiple
          :class="{
            form__select: true,
            form__select_type_multiple: true,
            form__select_error: $v.clientData.personalData.clientGroup.$error,
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
          v-model.trim="$v.clientData.personalData.doctor.$model"
          :class="{
            form__select: true,
            form__select_error: $v.clientData.personalData.doctor.$error,
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
          v-model.trim="clientData.personalData.notSendSms"
          class="form__invisible-checkbox"
          type="checkbox"
          group-name="personalData"
          name="notSendSms"
        >
        <span class="form__visible-checkbox" />
        <p class="form__text">Не отправлять СМС</p>
      </label>
    </fieldset>

    <fieldset
      v-show="actileFieldset === 1"
      class="form__fieldset"
    >
      <legend class="form__legend">
        Адрес
      </legend>

      <Input
        :value="clientData.address.index"
        placeholder="Индекс"
        :is-error="$v.clientData.address.index.$error"
        :error-message="errorMessage.address.index"
        type="text"
        group-name="address"
        name="index"
        maxlength="15"
        :handle-change="handleInputChange"
      />

      <Input
        :value="clientData.address.country"
        placeholder="Страна"
        :is-error="$v.clientData.address.country.$error"
        :error-message="errorMessage.address.country"
        type="text"
        group-name="address"
        name="country"
        maxlength="20"
        :handle-change="handleInputChange"
      />

      <Input
        :value="clientData.address.region"
        placeholder="Область"
        :is-error="$v.clientData.address.region.$error"
        :error-message="errorMessage.address.region"
        type="text"
        group-name="address"
        name="region"
        maxlength="20"
        :handle-change="handleInputChange"
      />

      <Input
        :value="clientData.address.city"
        placeholder="Город"
        :is-error="$v.clientData.address.city.$error"
        :error-message="errorMessage.address.city"
        type="text"
        group-name="address"
        name="city"
        maxlength="20"
        :handle-change="handleInputChange"
      />

      <Input
        :value="clientData.address.street"
        placeholder="Улица"
        :is-error="$v.clientData.address.street.$error"
        :error-message="errorMessage.address.street"
        type="text"
        group-name="address"
        name="street"
        maxlength="20"
        :handle-change="handleInputChange"
      />

      <Input
        :value="clientData.address.house"
        placeholder="Дом"
        :is-error="$v.clientData.address.house.$error"
        :error-message="errorMessage.address.house"
        type="text"
        group-name="address"
        name="house"
        maxlength="20"
        :handle-change="handleInputChange"
      />
    </fieldset>
    <fieldset
      v-show="actileFieldset === 2"
      class="form__fieldset"
    >
      <legend class="form__legend">
        Паспорт
      </legend>

      <InputContainer
        placeholder="Тип документа"
        :is-error="$v.clientData.passport.documentType.$error"
        :error-message="constErrorMessage.required"
      >
        <select
          v-model.trim="$v.clientData.passport.documentType.$model"
          :class="{
            form__select: true,
            form__select_error: $v.clientData.passport.documentType.$error,
          }"
          name="documentType"
        >
          <option>Паспорт</option>
          <option>Свидетельство о рождении</option>
          <option>Вод. удостоверение</option>
        </select>
      </InputContainer>


      <Input
        :value="clientData.passport.series"
        placeholder="Серия"
        :is-error="$v.clientData.passport.series.$error"
        :error-message="errorMessage.passport.series"
        type="text"
        group-name="passport"
        name="series"
        maxlength="4"
        :handle-change="handleInputChange"
      />

      <Input
        :value="clientData.passport.number"
        placeholder="Номер"
        :is-error="$v.clientData.passport.number.$error"
        :error-message="errorMessage.passport.number"
        type="text"
        group-name="passport"
        name="number"
        maxlength="6"
        :handle-change="handleInputChange"
      />

      <Input
        :value="clientData.passport.issuedBy"
        placeholder="Кем выдан"
        :is-error="$v.clientData.passport.issuedBy.$error"
        :error-message="errorMessage.passport.issuedBy"
        type="text"
        group-name="passport"
        name="issuedBy"
        maxlength="40"
        :handle-change="handleInputChange"
      />

      <Input
        :value="clientData.passport.dateOfIssue"
        placeholder="Дата выдачи"
        :is-error="$v.clientData.passport.dateOfIssue.$error"
        :error-message="errorMessage.passport.dateOfIssue"
        type="date"
        group-name="passport"
        name="dateOfIssue"
        :handle-change="handleInputChange"
      />
    </fieldset>
    <button
      class="form__submit"
      @click="submit"
    >
      {{ actileFieldset === (arrayFieldset.length - 1) ? 'Создать нового клиента': 'Далее' }}
    </button>
    <p
      v-show="isFormSent"
      class="form__text"
    >
      Новый клиент успешно создан
    </p>
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
      arrayFieldset: ['personalData','address','passport'],
      actileFieldset: 0,
      isFormSent: false,
      clientData: {
        personalData: {
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
        address: {
          index: null,
          country: null,
          region: null,
          city: null,
          street: null,
          house: null,
        },
        passport: {
          documentType: null,
          series: null,
          number: null,
          issuedBy: null,
          dateOfIssue: null,
        },
      },
      errorMessage: {
        personalData: {},
        address: {},
        passport: {},
      },
      constErrorMessage: {
        required: "Поле, обязательное для заполнения",
      },
    };
  },

   validations: {
      clientData: {
        personalData: {
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
        address: {
          index: {
            numeric,
          },
          country: {},
          region: {},
          city: {
            required,
          },
          street: {},
          house: {},
        },
        passport: {
          documentType: {
            required,
          },
          series: {
            numeric,
          },
          number: {
            numeric,
          },
          issuedBy: {},
          dateOfIssue: {
            required,
          },
      },
    },
  },
  methods: {
    submit(e) {
      e.preventDefault();
      const vCurrent = this.$v.clientData[this.arrayFieldset[this.actileFieldset]];
      vCurrent.$touch();
      if (!vCurrent.$invalid) {
        if (this.actileFieldset < this.arrayFieldset.length-1) this.actileFieldset++;
        else {
          this.isFormSent = true;
          // отправка данных
        }
      }
    },
    handleInputChange(e, groupName) {
      // обновление данных
      const name = e.target.name;
      this.clientData[groupName][name] = e.target.value;
      this.$v.clientData[groupName][name].$touch();

      // обновление сообщения об ошибке
      this.errorMessage[groupName][name] = this.getErrorMessage(groupName, name);
    },

    getErrorMessage(groupName, name) {
      const current = this.$v.clientData[groupName][name];
      if (!current.$error) {
        return '';
      } else {
          if (current.required !== undefined && !current.required){
            return this.constErrorMessage.required;
          } else if (current.numeric !== undefined && !current.numeric) {
              return 'Поле должно содержать только цифры';
          } else if (current.minLength !== undefined && !current.minLength) {
              return `Поле должно содержать не менее ${current.$params.minLength.min } символов`;
          }
          return 'Не допустимое значение';
        }
    }
  }
};
</script>

<style scoped lang="scss">
@import "./Form.sass";
</style>
