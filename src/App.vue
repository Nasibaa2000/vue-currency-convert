<script src="https://www.cbr-xml-daily.ru/money.js"></script>

<template>
  <div class="home">
   <div class="container">
     <!----<div class="input"> -->
      <div class="input_type">
        <input class="value" v-model="fromCurrencyValue" type="number"/> 
        <select class="select" v-model="fromCurrencyType" @change="convert">
          <option v-for="(value, key) of data" :key="value.ID" :value="key">{{ key }}</option>
        </select>
      </div>
      <img src="Vector.png">
      <div class="input_type">
        <input class="value" :value="toCurrencyValue" type="number">
        <select class="select" v-model="toCurrencyType" @change="convert">
          <option v-for="(value, key) of data" :key="value.ID" :value="key">{{ key }}</option>
        </select>
       
       <!----</div> -->
    </div>
 </div>
</div>
</template> 
  


<script>
   
 import axios from 'axios';
 export default {
  name:"App",
  data() {
     return{
      fromCurrencyValue: undefined,
      fromCurrencyType: undefined,
      toCurrencyValue: undefined,
      toCurrencyType: undefined,
      data: undefined
     };
  },
  methods: {
    convert() {
      if(this.validInput){
        const value1 = this.data[this.fromCurrencyType].Value
        const value2 = this.data[this.toCurrencyType].Value
        const ratio = value1 / value2;
        this.toCurrencyValue = (this.fromCurrencyValue * ratio).toFixed(2)
      }
    }
  },

  computed: {
    validInput() {
      return this.fromCurrencyValue && this.fromCurrencyType && this.toCurrencyType
    }
  },
  watch: {
    fromCurrencyValue() {
      this.convert()
    }
  },
  async mounted() {
    const response = await fetch(`https://www.cbr-xml-daily.ru/daily_json.js`)
    const {Valute} = await response.json()
    this.data = Valute
  }

  
 }

</script>


<style>

.container {
    display: inline-block;
    height: 100%;
    vertical-align: middle;
    content: "";
    margin: 32px;

}

.input_type {
   display: inline-block;
   vertical-align: middle;
   align-items: center;
   width: 255px;
   height: 46px;
   border-radius: 8px;
   padding: 0;
   border: 1px solid #D5DAE1;
   font-family: 'Noto Sans', sans-serif;
   font-size: 16px;
   vertical-align: middle;
   

}

.value {
   width: 114px;
   height: 24px;
   border: 0;
   margin: 11px 8px 11px 14px;
}

img {
   display: inline-block;
   vertical-align: middle;
   width: 20px;
   height: 14px;
   padding: 0 16px;
}

.select {
   width: 101px;
   height: 36px;
   margin: 5px 14px 5px 0;
   border: 0;
   border-radius: 61px;
   
   padding: 6px 12px 6px 12px;
   appearance: none !important;
   background: url(Vectorrrr.svg) no-repeat right;
   background-color: rgba(85, 105, 135, 0.08);
   background-position-x: calc(100% - 14px)
}


</style>