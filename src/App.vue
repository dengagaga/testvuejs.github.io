

<template>
  <div class="container">
    <h1 class="title-1">Настройте тариф</h1>
    <h3 class="title-3">
      Телефон
    </h3>
    <div class="input_all">
      <input type="number" class="input_phone" v-model="phone" placeholder="+7 (____) ___-__-__">
      <label for="" class="input_label">Обязательное поле</label>
      <span v-if="phoneErrorMessage.length > 0" class="error-message">{{ phoneErrorMessage }}</span>
    </div>
    <tariffsSlider @changePriceSlider="changePriceSlider" title="Минуты" :items="tariffsSliderMinutes" name="tariffsSliderMinutes" :min="1" :max="tariffsSliderMinutes.length" :def="3">
    </tariffsSlider>
    <tariffsSlider  @changePriceSlider="changePriceSlider" title="СМС" :black="true" :items="tariffsSliderSms" :min="1" name="tariffsSliderSms" :max="tariffsSliderSms.length" :def="2"></tariffsSlider>
    <tariffsSlider  @changePriceSlider="changePriceSlider" title="Интернет" :black="true" :items="tariffsSliderInternet" name="tariffsSliderInternet"  :min="1" :max="tariffsSliderInternet.length" :def="2"></tariffsSlider>
    <h3 class="title-3">
      Wi-Fi роутер
    </h3>
    <div class="input_all-checkbox">
      <input @change="changePrice" v-model="checkbox" type="checkbox" class="input_checkbox">
      <label for=""  class="input_checkbox-label">Аренда <strong>99</strong>  ₽/мес.</label>
    </div>
    <button class="form_btn" @click="validatePhone">
      <h4 class="title-4">
        {{ allPrice }} ₽
      </h4>
       в месяц
    </button>
  </div>
</template>
<script setup>
import tariffsSlider from './components/tariffsSlider.vue';
import { ref, computed } from 'vue';

const phone = ref('')
const checkbox = ref(false)
const phoneErrorMessage = ref(false)

const tariffsSliderMinutes = ref([{names: 200, price: 140}, {names: 350, price: 160}, {names: '600 минут', price: 180}, {names: 650, price: 200}])
const tariffsSliderSms = ref([{names: 0, price: 80}, {names: 50, price: 100}, {names: 100, price: 120}, {names: 150, price: 140}])
const tariffsSliderInternet = ref([{names: 5, price: 180}, {names: 15, price: 200}, {names: 30, price: 220}, {names: 35, price: 240}])

const changePrice = !checkbox.value

const firstInputValue = ref({names: '600 минут', price: 180});
const secondInputValue = ref({names: 50, price: 100});
const thirdInputValue = ref({names: 15, price: 200});

const allPrice = computed(() => firstInputValue.value.price + secondInputValue.value.price + thirdInputValue.value.price + (checkbox.value ? 99 : 0));

const changePriceSlider = (check ,items, name ) =>  {
  if (name == 'tariffsSliderMinutes') {
    firstInputValue.value = items[check - 1]
  }
  if (name == 'tariffsSliderSms') {
    secondInputValue.value = items[check - 1]
  }
  if (name == 'tariffsSliderInternet') {
    thirdInputValue.value = items[check - 1]
  }
}

const validatePhone = () => {
      if (phone.value.toString().length != 11) {        
        phoneErrorMessage.value = 'Неверный формат номера телефона.';
      }
      else if (phone.value.toString()[0] != 7) {
        phoneErrorMessage.value = 'Номер телефона должен начинаться с 7';
      }
      else {
        phoneErrorMessage.value = '';
        alert(JSON.stringify({
        phone: phone.value,
        minutes: firstInputValue.value,
        sms: secondInputValue.value,
        internet: thirdInputValue.value,
        RentСheckbox: checkbox.value,
        allPrice: allPrice.value
      }))
      }
}


</script>
<style>
.input_all {
  display: flex;
  flex-direction: column;
  gap: 10px;
  margin-bottom: 90px;

}
.input_label {
  color: var(--color-little);
  font-size: 12px;
  font-weight: 400;
}
.input_phone {
  border: 1px solid var(--border);
  background-color: #fff;
  height: 60px;
  border-radius: 8px;
  padding: 18px 16px;
  max-width: 368px;
  width: 100%;
}
.input_all-checkbox {
  display: flex;
  gap: 15px;
  align-items: center;
  margin-bottom: 90px;

}
.input_checkbox {
  width: 24px;
  height: 24px;
}
.input_checkbox-label {
  font-size: 24px;

  font-weight: 400;
}
.form_btn {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 90px;
  max-width: 250px;
  background-color: var(--bgc-btn);
  width: 100%;
  color: #fff;
  gap: 5px;
  border-radius: 15px;
  transition: all .3s;
}
.form_btn:hover {
  opacity: .8;
}
.error-message {
  color: red;
}
</style>
