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
  </div>
</template>

<script setup>
import { ref, watch } from 'vue';

const EnteredData= ref('')
const emit= defineEmits(['emitEnteredData']);
const props= defineProps({
  inputType:{
    type: String,
    default: ()=>('Url')
  }
});

watch(()=> props.inputType, ()=>{
  EnteredData.value='';
})

watch(EnteredData, (newEnteredData)=>{
  // console.log(newEnteredData);
  emit('emitEnteredData', newEnteredData)
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