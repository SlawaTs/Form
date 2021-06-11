<template>
  <form class="Forms" @submit.prevent="submitHandler">
    <div class="Attributes">
      <div>Фамилия*</div>
      <input type="text"
             v-model="surname"
             @input="$v.surname.$touch()"
             :class="{invalid: ($v.surname.$dirty && !$v.surname.required) || ($v.surname.$dirty && !$v.surname.alpha)}">
      <small class="pattern"
             v-if="$v.surname.$dirty && !$v.surname.required">Поле не должно быть пустым</small>
      <small class="pattern"
             v-else-if="$v.surname.$dirty && !$v.surname.alpha">Введите коректные даные</small>

      <div>Имя*</div>
      <input type="text"
             v-model="name"
             @input="$v.name.$touch()"
             :class="{invalid: ($v.name.$dirty && !$v.name.required) || ($v.name.$dirty && !$v.name.alpha)}">
      <small class="pattern"
             v-if="$v.name.$dirty && !$v.name.required">Поле не должно быть пустым</small>
      <small class="pattern"
             v-else-if="$v.name.$dirty && !$v.name.alpha">Введите коректные даные</small>

      <div>Отчество</div>
      <input type="text"
             v-model="patronymic"
             @input="$v.patronymic.$touch()">
      <small class="pattern"
             v-if="$v.patronymic.$dirty && !$v.patronymic.alpha">Введите коректные даные</small>

      <div>Дата рождения*</div>
      <input type="date"
             v-model="dateOfBirth"
             @input="$v.dateOfBirth.$touch()"
             :class="{invalid: ($v.dateOfBirth.$dirty && !$v.dateOfBirth.required)}">
      <small class="pattern"
             v-if="$v.dateOfBirth.$dirty && !$v.dateOfBirth.required">Поле не должно быть пустым</small>

      <div>Номер телефона*</div>
      <input type="text"
             placeholder="Номер начинается с 7"
             v-model="phone"
             @input="$v.phone.$touch()"
             :class="{invalid: ($v.phone.$dirty && !$v.phone.required) || ($v.phone.$dirty && !$v.phone.alpha)}">
      <small class="pattern"
             v-if="$v.phone.$dirty && !$v.phone.required">Поле не должно быть пустым</small>
      <small class="pattern"
             v-else-if="$v.phone.$dirty && !$v.phone.alpha">Введите коректные даные</small>

      <div>
        <label>Пол:</label>
        <label><input type="radio" name="gender" value="man" v-model="gendere">М</label>
        <label><input type="radio" name="gender" value="woman" v-model="gendere">Ж</label>
      </div>

      <label>Группа клиентов*</label>
      <select multiple size="3"
              v-model="customerGroup"
              @input="$v.customerGroup.$touch()"
              :class="{invalid: ($v.customerGroup.$dirty && !$v.customerGroup.required)}">
        <option value="vip">VIP</option>
        <option value="problem">Проблемные</option>
        <option value="omc">OMC</option>
      </select>
      <small class="pattern"
             v-if="$v.customerGroup.$dirty && !$v.customerGroup.required">Поле не должно быть пустым</small>

      <label>Лечащий врач:</label>
      <select v-model="doctor">
        <option value="ivanov">Иванов</option>
        <option value="zaharov">Захаров</option>
        <option value="chernisheva">Чернышева</option>
      </select>

      <div>
        <label>Не отправлять СМС</label>
        <input type="checkbox" v-model="notification">
      </div>
    </div>
    <div class="Address">
      <label>Адрес:</label>
      <input type="text"
             placeholder="Индекс"
             v-model="index"
             @input="$v.index.$touch()">
      <small class="pattern"
             v-if="$v.index.$dirty && !$v.index.alpha">Введите коректные даные</small>

      <input type="text"
             placeholder="Страна"
             v-model="country"
             @input="$v.country.$touch()">
      <small class="pattern"
             v-if="$v.country.$dirty && !$v.country.alpha">Введите коректные даные</small>

      <input type="text"
             placeholder="Область"
             v-model="region"
             @input="$v.region.$touch()">
      <small class="pattern"
             v-if="$v.region.$dirty && !$v.region.alpha">Введите коректные даные</small>

      <input type="text"
             placeholder="Город*"
             v-model="city"
             @input="$v.city.$touch()"
             :class="{invalid: ($v.city.$dirty && !$v.city.required) || ($v.city.$dirty && !$v.city.alpha)}">
      <small class="pattern"
             v-if="$v.city.$dirty && !$v.city.required">Поле не должно быть пустым</small>
      <small class="pattern"
             v-else-if="$v.city.$dirty && !$v.city.alpha">Введите коректные даные</small>

      <input type="text"
             placeholder="Улица"
             v-model.trim="street"
             @input="$v.street.$touch()">
      <small class="pattern"
             v-if="$v.street.$dirty && !$v.street.alpha">Введите коректные даные</small>

      <input type="text"
             placeholder="Дом"
             v-model="house"
             @input="$v.house.$touch()">
      <small class="pattern"
             v-if="$v.house.$dirty && !$v.house.alpha">Введите коректные даные</small>
    </div>
    <div class="Passport">
      <label>Тип документа*</label>
       <select v-model="documentType"
               @input="$v.documentType.$touch()"
               :class="{invalid: ($v.documentType.$dirty && !$v.documentType.required)}">
         <option value="passport">Паспорт</option>
         <option value="birthCertificate">Свидетельство о рождении</option>
         <option value="driverLicense">Вод. удостоверение</option>
      </select>
      <small class="pattern"
             v-if="$v.documentType.$dirty && !$v.documentType.required">Поле не должно быть пустым</small>

     <input type="text"
            placeholder="Серия"
            v-model="documentSeries"
            @input="$v.documentSeries.$touch()">

     <input type="text"
            placeholder="Номер"
            v-model="documentNumber"
            @input="$v.documentNumber.$touch()">
      <small class="pattern"
             v-if="$v.documentNumber.$dirty && !$v.documentNumber.alpha">Введите коректные даные</small>

     <input type="text"
            placeholder="Кем выдан"
            v-model="issuedBy">

     <label>Дата выдачи*</label>
      <input type="date"
             v-model="dateOfIssue"
             @input="$v.dateOfIssue.$touch()"
             :class="{invalid: ($v.dateOfIssue.$dirty && !$v.dateOfIssue.required)}">
      <small class="pattern"
             v-if="$v.dateOfIssue.$dirty && !$v.dateOfIssue.required">Поле не должно быть пустым</small>

    </div>
    <p>*Поле обязательное для заполнения.</p>
    <button type="submit" :disabled="$v.$invalid">Save</button>
  </form>
</template>
<script>
import {required} from 'vuelidate/lib/validators'
export default {
  name: 'forms',
  data() {
    return {
      surname: '',
      name: '',
      patronymic: '',
      phone:'',
      dateOfBirth: '',
      gendere:'man',
      customerGroup:[],
      doctor:'',
      notification:'',
      index:'',
      country:'',
      region:'',
      city:'',
      street:'',
      house:'',
      documentType:'',
      documentSeries:'',
      documentNumber:'',
      issuedBy:'',
      dateOfIssue:'',
    }

  },
  validations:{
    surname: {required,alpha: val => /^[а-яё]*$/i.test(val)},
    name: {required,alpha: val => /^[а-яё]*$/i.test(val)},
    patronymic: {alpha: val => /^[а-яё]*$/i.test(val)},
    dateOfBirth: {required},
    phone:{required,alpha: val => /^[7]\d{3}-?\d{3}-?\d{2}-?\d{2}$/.test(val)},
    gendere:{},
    customerGroup:{required},
    doctor:{},
    notification:{},
    index:{alpha: val => /^[0-9]*$/i.test(val)},
    country:{alpha: val => /^[а-яё]*$/i.test(val)},
    region:{alpha: val => /^[а-яё]*$/i.test(val)},
    city:{required,alpha: val => /^[а-яё]*$/i.test(val)},
    street:{alpha: val => /^[0-9]*?[а-яё]*$/i.test(val)},
    house:{alpha: val => /^[0-9]*[/]?[0-9]?[а-я]?$/i.test(val)},
    documentType:{required},
    documentSeries:{},
    documentNumber:{alpha: val => /^[0-9]*$/i.test(val)},
    issuedBy:{},
    dateOfIssue:{required},
  },
  methods:{
    submitHandler(){
      alert('Новый клиент успешно создан')
    }
  }
}
</script>
<style>
.Forms{
  margin: 40px;
  line-height: 25px;
}
.Attributes{
  width: 200px;
  display: grid;
}
.Address{
  width: 200px;
  display: grid;
}
.Passport{
  width: 200px;
  display: grid;
}
.pattern{
  color: red;
}
</style>