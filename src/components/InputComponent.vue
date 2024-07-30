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
        <label for="">Network Name</label>
        <input v-model="EnteredWifiData.networkName" type="text">
        
        <label for="">Network Password</label>
        <input v-model="EnteredWifiData.networkPassword " type="password">

        <label for="">Type of encryption*</label>
        <select v-model="EnteredWifiData.encryptionType"  id="">
          <option value="WPA">WPA</option>
          <option value="WPA1">WPA1</option>
          <option value="WPA2">WPA2</option>
          <option value="WPA3">WPA3</option>
        </select>

        <input type="submit" value="Generate" @click="handleWifiForm">
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
</style>