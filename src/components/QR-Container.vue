<template>
  <div class="container">
    <div class="item item1">
      <QRbutton @click="changeButtonStatus('Text')" :class="ActiveButton === 'Text' ? 'buttonActive' : ''" buttonName="Text" Icon="fa-solid fa-file-lines"/>
      <QRbutton @click="changeButtonStatus('Url')" :class="ActiveButton === 'Url' ? 'buttonActive' : ''" buttonName="Url" Icon="fa-solid fa-globe"/>
      <QRbutton @click="changeButtonStatus('WiFi')" :class="ActiveButton === 'WiFi' ? 'buttonActive' : ''" buttonName="Wi-Fi" Icon="fa-solid fa-wifi"/>
      <QRbutton disabled="true" @click="changeButtonStatus('Email')" :class="ActiveButton === 'Email' ? 'buttonActive' : ''" buttonName="Email" Icon="fa-solid fa-envelope"/>
      <QRbutton disabled="true" @click="changeButtonStatus('Pdf')" :class="ActiveButton === 'Pdf' ? 'buttonActive' : ''" buttonName="Pdf" Icon="fa-solid fa-file-pdf"/>
      <QRbutton disabled="true" @click="changeButtonStatus('Sms')" :class="ActiveButton === 'Sms' ? 'buttonActive' : ''" buttonName="SMS" Icon="fa-solid fa-sms"/>
    </div>
    <div class="item item2">
      <QRDisplayerComponent :qrUrl="OriginalQrCodeImage_File" :key="OriginalQrCodeImage_File"/>
      <a id="downloadButton" :href="OriginalQrCodeImage_File" download="qr.png"><font-awesome-icon icon="fa-solid fa-download" style="margin-right: 5px;"/> Download QR</a>
    </div>
    <div class="item item3">
      <InputComponent :inputType="inputType"  @emitEnteredData="handleEmit"/>
    </div>
  </div>
</template>

<script setup>
import { ref, watch } from 'vue';
import QRbutton from './button.vue';
import InputComponent from './InputComponent.vue';
import QRDisplayerComponent from './QRDisplayer-Component.vue';

const ActiveButton= ref('Text')
const InputedData= ref('');
const inputType= ref('Text');
const OriginalQrCodeImage_File=ref();

//function to handle api call
async function callApi(apiEndPoint, Method, Data){
  try{
    const response= await fetch(apiEndPoint, {
      method: Method,
      headers: {
        'Content-Type': 'application/json'
      },
      body: JSON.stringify({
      data: Data
      })
    });

    if(!response.ok){
      throw new Error(`Response Status: ${response.status}`);
    } else{
      const json= await response.json();
      const imageUrl= json.qr_url;
      // call image url endpoint & convert its response (which is image) to blob object.
      // blob(binary large object) object and file object work similar 
      const res= await fetch(imageUrl);
      const blob= await res.blob();
      //const file = new File([blob], 'image', {type: blob.type});
      readFile(blob)
    };

  }catch(error){
    console.log(error.message);
  }
}

// read file
function readFile(input){
  const fileread= new FileReader();
  fileread.readAsDataURL(input);

  fileread.addEventListener('load', ()=>{
    const res= fileread.result;
    OriginalQrCodeImage_File.value=res;
  })
}


function handleEmit(data){
  InputedData.value= data;

  // Determining whether the variable is object or not
  if(InputedData.value instanceof Object){

    // checking the value of type property to match provided "cases".
    switch (InputedData.value.type) {
      case 'wifi':
        console.log("This object has type: wifi");
        // formatting data to a specific string data format for wifi network
        let data= `WIFI:S:${InputedData.value.networkName};T:${InputedData.value.encryptionType};P:${InputedData.value.networkPassword};;`
        callApi('http://127.0.0.1:5000/generate-QrCode', 'POST', data)
        break;
      case 'email':
        console.log("This is object email");
        break;
      case 'pdf':
        // Handle pdf case
        break;
      case 'sms':
        // Handle sms case
        break;
      case 'vcard':
        // Handle vcard case
        break;
      default:
        console.log("Unknown Type");
        break;
    }
  } else{
    callApi('http://127.0.0.1:5000/generate-QrCode', 'POST', InputedData.value);
  }
}


function changeButtonStatus(ButtonName){
  ActiveButton.value= ActiveButton.value === ButtonName ? null : ButtonName
  inputType.value= ButtonName;
}

</script>

<style scoped>
.container{
    display: grid;
    grid-template-columns: 1.5fr 1fr;
    grid-template-rows: repeat(2, minmax(100px, auto));
    width: 100%;
    border: none;
    border-radius: 10px;
    padding: 0;
    box-shadow: 0px 0px 200px -50px green, 0 -3em 200px mediumpurple;
    margin-bottom: 250px;
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
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    padding-top: 30px;
    /* align-items: center; */
}

.container .item3{
    /* background-color: yellow; */
    
}

.buttonActive{
    border: 2px solid blue;
}

#downloadButton{
  display: block;
  height: 50px;
  padding: 11px;
  margin-top: 25px;
  margin-bottom: 25px;
  border: none;
  border-radius:15px;
  color: aliceblue;
  cursor: pointer;
  background-color: rgb(87, 87, 255);
  transition: 0.5s;
}

#downloadButton:hover{
  background-color: rgb(64, 64, 191);
}

@media only screen and (max-width: 750px) {
  .container {
        grid-template-columns: 1fr; /* Make columns into rows */
        grid-template-rows: auto; /* Adjust row sizing */
    }

    .container .item1 {
        border-radius: 10px 10px 0 0; /* Adjust border radius */
    }

    .container .item2 {
        grid-row-start: 3;
        grid-row-end: 4;
        grid-column-start: 1;
        grid-column-end: 2;
        border-left: none;
        border-top: 1px solid #c5c3cf;
    }

    .container .item3 {
        grid-row-start: 2;
        grid-row-end: 3;
        padding-bottom: 50px;
    }
}
</style>