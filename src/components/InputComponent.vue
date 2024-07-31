<template>
  <div class="inputContainer">
    <div v-if="inputType === 'Text'">
      <label class="input-label">message*</label>
      <textarea v-model="EnteredData" class="input" id="text" cols="80" rows="3" placeholder="Enter some text"></textarea>
    </div>

    <div v-if="inputType === 'Url'">
      <label class="input-label">Website Url*</label>
      <input v-model="EnteredData" type="text" id="Url" class="input" placeholder="E.g. https://www.jeevanrawal.com.np/">
    </div>

    <div v-if="inputType === 'WiFi'">
      <form @submit.prevent="onSubmit">
        <div class="formContainer">
          <div class="formitems-wrapper">
            <label class="formLabel" for="">Network Name</label>
            <input v-model="EnteredWifiData.networkName" type="text">
          </div>
          
          <div class="formitems-wrapper">
            <label class="formLabel" for="">Network Password</label>
            <input v-model="EnteredWifiData.networkPassword " type="password">
          </div>
  
          <div class="formitems-wrapper">
            <label class="formLabel">Type of encryption*</label>
            <select v-model="EnteredWifiData.encryptionType" name="encryptionType">
              <option value="WPA">WPA</option>
              <option value="WPA1">WPA1</option>
              <option value="WPA2">WPA2</option>
              <option value="WPA3">WPA3</option>
            </select>
          </div>
  
          <input id="GenerateButton" type="submit" value="Generate QR Code" @click="handleWifiForm">
        </div>
      </form>
    </div>
  </div>
</template>

<script setup>
import { ref, watch } from 'vue';

const EnteredData= ref('')
const EnteredWifiData= ref({
  type:'wifi',
  networkName:'',
  networkPassword:'',
  encryptionType:''
})
const emit= defineEmits(['emitEnteredData']);
const props= defineProps({
  inputType:{
    type: String,
    default: ()=>('Url')
  }
});

function handleWifiForm(){
  // console.log(EnteredWifiData.value);
  emit('emitEnteredData', EnteredWifiData.value)
}

watch(()=> props.inputType, ()=>{
  EnteredData.value='';
  
  //emptying object
  // for (let key in EnteredWifiData) {
  //       EnteredWifiData[key]='';
  // }
})

watch(EnteredData, (newEnteredData)=>{
  // console.log(newEnteredData);
  if(newEnteredData !== ''){
    emit('emitEnteredData', newEnteredData)
  }
})
</script>

<style scoped>
.input-label{
    display: block;
}

.input{
  width: 100%;
  font-family:Arial, Helvetica, sans-serif;
  font-weight: 100;
  font-size: 16px;
  padding: 0px 6px 0px 10px;
  border-radius:4px;
  border: 2px solid #dbdada;
  transition: 0.5s;
}

.input:hover{
  border: 2px solid black;
}

#Url{
  height: 50px;
}

.formContainer{
  display: flex;
  flex-wrap: wrap;
  width: 100%;
  margin-top: 15px;
  font-family:Arial, Helvetica, sans-serif;

  /* justify-content: space-between; */
}

.formitems-wrapper{
  margin-left: 15px;
  margin-bottom: 30px;
}

.formitems-wrapper input{
  width: 350px;
  min-width: 50px;
  padding: 15px;
  border-radius:4px;
  border: 2px solid #dbdada;
  height: 40px;
  transition: 0.5s;
}

.formitems-wrapper select{
  width: 100px;
  height: 40px;
  padding-left: 15px;
  border-radius:4px;
  border: 2px solid #dbdada;
  transition: 0.5s;
}

.formitems-wrapper input:hover, .formitems-wrapper select:hover{
  border: 2px solid black;
}

.formLabel{
  display: block;
  
}

#GenerateButton{
  height: 50px;
  margin-left: 63px;
  margin-top: 25px;
  padding: 10px;
  border-radius:10px;
  border: none;
  background-color: rgb(87, 87, 255);
  color: aliceblue;
  transition: 0.5s;
}

#GenerateButton:hover{
  background-color: rgb(64, 64, 191);
}
</style>