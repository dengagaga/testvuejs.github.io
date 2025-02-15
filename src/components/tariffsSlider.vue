<template>
    <div class="slider-container">
        <h3 class="title-3">{{title}}</h3>
          <label class="slider">
            <input @change="$emit('changePriceSlider', sliderValue, items, name)" type="range" :min="min" :max="max" v-model="sliderValue" :class="black  ?  'level level-black' :'level'">
          </label>
          <div class="slider-slot" >
              <p v-for="item in items" :key="item" class="slider-slot-number">
                  {{ item.names }}
              </p>
          
          </div>
    </div>
</template>
<script setup>
import { onMounted, ref } from 'vue';
const props = defineProps({
  title: String,
  items: Array,
  name: String,
  black: Boolean,
  min: Number,
  max: Number,
  def: Number,
});
const sliderValue = ref(props.def)



</script>

<style>
.slider-container {
  margin-bottom: 90px;
}
.slider-slot {
  display: flex;
  justify-content: space-between;
}
.slider-slot-number {
  font-size: 24px;
  font-weight: 500;
  margin-top: 30px;
  margin-left: 25px;
}
.slider-input {
  background-color: var(--bgc-btn);
}


.slider {
  cursor: pointer;
  display: -webkit-inline-box;
  display: -ms-inline-flexbox;
  display: inline-flex;
  width: 100%;
  height: 60px;

  -webkit-box-orient: horizontal;
  -webkit-box-direction: reverse;
  -ms-flex-direction: row-reverse;
  flex-direction: row-reverse;
  -webkit-box-align: center;
  -ms-flex-align: center;
  align-items: center;
}

.slider .volume {
  display: inline-block;
  vertical-align: top;
  margin-right: 15px;
  color:rgb(82, 82, 82);
  width: 25px;
  height: auto;
}

.slider .level {
  -webkit-appearance: none;
  -moz-appearance: none;
  appearance: none;
  width: 100%;
  height: 10px;
  background: var(--bgc-btn);
  border-radius: 999px;
  -webkit-transition: height .1s;
  -o-transition: height .1s;
  transition: height .1s;
  cursor: inherit;
}

.level-black  {
  background: #000000!important;
}

.slider .level::-webkit-slider-thumb {
  -webkit-appearance: none;
  width: 60px;
  height: 60px;
  border-radius: 50%;
  background: url(../assets/img.png);
  background-position: center;
  background-repeat: no-repeat;
}
.level-black::-webkit-slider-thumb  {
  background: url(../assets/img2.png)!important;
}

</style>