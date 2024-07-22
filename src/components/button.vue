<template>
    <button> <div style=" display: inline-block; margin-right: 5px; margin-left: 5px; background-color: #edeaea; width: 35px; text-align: center; border-radius: 3px;"><font-awesome-icon :icon="Icon"/></div> {{ props.buttonName }}</button>
</template>

<script setup>
const props= defineProps({
    buttonName: {
        type: String,
        default: ()=>("button")
    },
    Icon:{
        type: String,
        default: ()=>("fa-solid fa-infinity")
    },
})
</script>

<style scoped>

button{
    width: 165px;
    height: 55px;
    margin-right: 17px;
    margin-bottom: 10px;
    text-align: start;
    background-color: white;
    border: 2px solid #dbdada;
    border-radius: 8px;
    font-family:'Times New Roman', Times, serif;
    /* font-weight: 200; */
    transition: border 0.2s;
}

button:hover{
    border: 2px solid blue;
}
</style>