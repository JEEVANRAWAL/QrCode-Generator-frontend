<script setup>
//example components
import NavbarDefault from "../../examples/navbars/NavbarDefault.vue";
import DefaultFooter from "../../examples/footers/FooterDefault.vue";
import Header from "../../examples/Header.vue";


// sections
import HomePageCounter from "./Sections/HomePageCounter.vue";
import QRContainer from "../../components/QR-Container.vue";


//images
import HeaderBgImage from "@/assets/img/qrcode-header.jpg";

//hooks
const body = document.getElementsByTagName("body")[0];

</script>

<template>
  <div class="container position-sticky z-index-sticky top-0">
    <div class="row">
      <div class="col-12">
        <NavbarDefault :sticky="true" />
      </div>
    </div>
  </div>
  <Header>
    <div
      class="page-header min-vh-75"
      :style="`background-image: url(${HeaderBgImage})`"
      loading="lazy"
    >
      <div class="container">
        <div class="row">
          <div class="col-lg-7 text-center mx-auto position-relative">
            <h1
              class="text-white pt-3 mt-n5 me-2"
              :style="{ display: 'inline-block ' }"
            >
              Generate Your QRCODE
            </h1>
            <p class="lead text-white px-5 mt-3" :style="{ fontWeight: '500' }">
              Create your own QR code and boost your business and ideas
            </p>
          </div>
        </div>
      </div>
    </div>
  </Header>

  <div class="card card-body blur shadow-blur mx-3 mx-md-4 mt-n6">
    <HomePageCounter />
    <QRContainer />

  </div>
  <DefaultFooter />
</template>
