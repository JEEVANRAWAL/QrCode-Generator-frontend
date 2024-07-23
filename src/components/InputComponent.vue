<template>
  <div class="inputContainer">
    <label class="input-label">message*</label>
    <textarea v-model="EnteredData" name="text" id="text" cols="80" rows="3" placeholder="Enter some text"></textarea>
  </div>
</template>

<script setup>
import { ref, watch } from 'vue';

const EnteredData= ref('')
const emit= defineEmits(['emitEnteredData'])

watch(EnteredData, (newEnteredData)=>{
  // console.log(newEnteredData);
  emit('emitEnteredData', newEnteredData)
})
</script>

<style scoped>
.input-label{
    display: block;
}

#text{
  font-family:Arial, Helvetica, sans-serif;
  font-weight: 100;
  font-size: 16px;
  padding: 0px 6px 0px 10px;
  border-radius:4px;
  border: 2px solid #dbdada;
  transition: 0.5s;
}

#text:hover{
  border: 2px solid black;
}
</style>