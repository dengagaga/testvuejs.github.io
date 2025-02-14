

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
    <tariffsSlider  @changePriceSlider="changePriceSlider"  title="Минуты" :array="[200, 350, 600, 650]" :min="1"  :max="4" :default="3">
    </tariffsSlider>
    <tariffsSlider @changePriceSliderBlackOne="changePriceSliderBlackOne" title="СМС" :array="[0, 50, 100, 150]" :black="true" :min="1" :max="4" :default="2"></tariffsSlider>
    <tariffsSlider @changePriceSliderBlackTwo="changePriceSliderBlackTwo" title="Интернет" :array="[5, 15, 30, 35]" :black="true" :min="1" :max="4" :default="2"></tariffsSlider>
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
import { ref } from 'vue';

const phone = ref('')
const allPrice = ref(480)
const checkbox = ref(false)
const phoneErrorMessage = ref(false)
const def = ref(3)
const defDrkOne = ref(2)
const defDrkTwo = ref(2)
const changePriceSlider = (check) => {
  if (def.value > check) {
    if ((def.value  - Number(check)) == 1) {
      allPrice.value = allPrice.value - 20
      def.value = check
    }
    if ((def.value  - Number(check)) == 2) {
      allPrice.value = allPrice.value - 40
      def.value = check
    }
    if ((def.value  - Number(check)) == 3) {
      allPrice.value = allPrice.value - 60
      def.value = check
    }
   
  }
  if (def.value < check) {
    if ((Number(check)  - def.value) == 1) {
      allPrice.value = allPrice.value + 20
    def.value = check
    }
    if ((Number(check)  - def.value) == 2) {
      allPrice.value = allPrice.value + 40
    def.value = check
    }
    if ((Number(check)  - def.value) == 3) {
      allPrice.value = allPrice.value + 60
      def.value = check
    }
  }
}
const changePriceSliderBlackOne = (check) => {
  
  if (defDrkOne.value > check) {
    if ((defDrkOne.value  - Number(check)) == 1) {
      allPrice.value = allPrice.value - 20
      defDrkOne.value = check
    }
    if ((defDrkOne.value  - Number(check)) == 2) {
      allPrice.value = allPrice.value - 40
      defDrkOne.value = check
    }
    if ((defDrkOne.value  - Number(check)) == 3) {
      allPrice.value = allPrice.value - 60
      defDrkOne.value = check
    }
  }
  if (defDrkOne.value < check) {
    if ((Number(check)  - defDrkOne.value) == 1) {
      allPrice.value = allPrice.value + 20
      defDrkOne.value = check
    }
    if ((Number(check)  - defDrkOne.value) == 2) {
      allPrice.value = allPrice.value + 40
      defDrkOne.value = check
    }
    if ((Number(check)  - defDrkOne.value) == 3) {
      allPrice.value = allPrice.value + 60
      defDrkOne.value = check
    }
  }
}
const changePriceSliderBlackTwo = (check) => {
  if (defDrkTwo.value > check) {
    if ((defDrkTwo.value  - Number(check)) == 1) {
      allPrice.value = allPrice.value - 20
      defDrkTwo.value = check
    }
    if ((defDrkTwo.value  - Number(check)) == 2) {
      allPrice.value = allPrice.value - 40
      defDrkTwo.value = check
    }
    if ((defDrkTwo.value  - Number(check)) == 3) {
      allPrice.value = allPrice.value - 60
      defDrkTwo.value = check
    }
   
  }
  if (defDrkTwo.value < check) {
    if ((Number(check)  - defDrkTwo.value) == 1) {
      allPrice.value = allPrice.value + 20
      defDrkTwo.value = check
    }
    if ((Number(check)  - defDrkTwo.value) == 2) {
      allPrice.value = allPrice.value + 40
      defDrkTwo.value = check
    }
    if ((Number(check)  - defDrkTwo.value) == 3) {
      allPrice.value = allPrice.value + 60
      defDrkTwo.value = check
    }
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
        minutes: def.value,
        sms: defDrkOne.value,
        internet: defDrkTwo.value,
        RentСheckbox: checkbox.value,
        allPrice: allPrice.value
      }))
      }

     
}

const changePrice = () => {
  if (checkbox.value) {
    allPrice.value = 480 + 99
  } else    {
    allPrice.value = 480
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
