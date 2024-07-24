<template>
  <div class="container">
    <div class="item item1">
      <QRbutton @click="changeButtonStatus('Text')" :class="ActiveButton === 'Text' ? 'buttonActive' : ''" buttonName="Text" Icon="fa-solid fa-file-lines"/>
      <QRbutton @click="changeButtonStatus('Url')" :class="ActiveButton === 'Url' ? 'buttonActive' : ''" buttonName="Url" Icon="fa-solid fa-globe"/>
      <QRbutton @click="changeButtonStatus('WiFi')" :class="ActiveButton === 'WiFi' ? 'buttonActive' : ''" buttonName="Wi-Fi" Icon="fa-solid fa-wifi"/>
      <QRbutton @click="changeButtonStatus('Email')" :class="ActiveButton === 'Email' ? 'buttonActive' : ''" buttonName="Email" Icon="fa-solid fa-envelope"/>
      <QRbutton @click="changeButtonStatus('Pdf')" :class="ActiveButton === 'Pdf' ? 'buttonActive' : ''" buttonName="Pdf" Icon="fa-solid fa-file-pdf"/>
      <QRbutton @click="changeButtonStatus('Sms')" :class="ActiveButton === 'Sms' ? 'buttonActive' : ''" buttonName="SMS" Icon="fa-solid fa-sms"/>
    </div>
    <div class="item item2">item 2</div>
    <div class="item item3">
      <InputComponent  @emitEnteredData="handleEmit"/>
    </div>
  </div>
</template>

<script setup>
import { ref, watch } from 'vue';
import QRbutton from './button.vue';
import InputComponent from './InputComponent.vue';

const ActiveButton= ref('Text')
const InputData= ref('');
const inputType= ref('');

function handleEmit(data){
  InputData.value= data;
  console.log("log from parent: "+ InputData.value);
}

function changeButtonStatus(ButtonName){
  ActiveButton.value= ActiveButton.value === ButtonName ? null : ButtonName
  inputType.value= ButtonName;
}

</script>

<style scoped>
.container{
    display: grid;
    grid-template-columns: 2fr 1fr;
    grid-template-rows: repeat(2, minmax(100px, auto));
    width: 100%;
    border: none;
    border-radius: 10px;
    padding: 0;
    box-shadow: 0px 0px 200px -50px green, 0 -3em 200px mediumpurple;
    /* box-shadow: 0px 0px 200px -100px green */
}

.container .item{
  padding: 10px 10px 10px 20px;
}

.container .item1{
    background-color: #edeaea;
    border-bottom: 1px solid #c5c3cf;
    border-radius: 10px 0 0 0;
}

.container .item2{
    /* background-color: red; */
    grid-row-start: 1;
    grid-row-end: 3;
    grid-column-start: 2;
    grid-column-end: 3;
    border-left: 1px solid #c5c3cf;
}

.container .item3{
    /* background-color: yellow; */
    
}

.buttonActive{
    border: 2px solid blue;
}
</style>