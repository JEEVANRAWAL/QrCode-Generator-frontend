<template>
<div class="imageBox">
    <img v-if="QRCodeUrl" :src="QRCodeUrl" alt="image">
    <font-awesome-icon v-if="QRCodeUrl === ''" class="qrcodeIcon" icon="fa-solid fa-qrcode"/>
</div>
</template>

<script setup>
// import demoImage from "@/assets/img/bruce-mars.jpg";
import { ref } from "vue";

const props= defineProps({
    qrUrl:{
        type: String,
        default: ()=> ('')
    }
})

const QRCodeUrl= ref(props.qrUrl);
</script>

<style scoped>
.imageBox{
    position: relative;
    width: 250px;
    height: 280px;
    border: 2px solid #dbdada;
    overflow: hidden;
    border-radius: 5px;
}

.imageBox img{
    position: absolute;
    width: 100%;
    height: 100%;
    top: 0px;
    left: 0px;
    object-fit: cover;
}

.imageBox .qrcodeIcon{
    position: absolute;
    width: 50%;
    height: 50%;
    top: 25%;
    left: 25%;
    /* object-fit: cover; */
}
</style>