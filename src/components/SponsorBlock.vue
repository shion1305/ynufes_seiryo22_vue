<script setup>
// Import Swiper Vue.js components
import {Swiper, SwiperSlide} from 'swiper/vue';
import {event} from "vue-gtag";
// Import Swiper styles
import 'swiper/css';
import 'swiper/css/autoplay'

// import Swiper core and required modules
import SwiperCore, {Autoplay} from 'swiper';
import axios from "axios";
import store from "@/store";
// install Swiper modules
SwiperCore.use([Autoplay]);

const randomList = function (rand) {
  return rand.map(value => ({value, sort: Math.random()}))
      .sort((a, b) => a.sort - b.sort)
      .map(({value}) => value);
  // return rand.sort(function () {
  //   return 0.5 - Math.random()
  // });
}

const access = async function (id) {
  if (process.env.NODE_ENV === "production") {
    event("sponsor:click", {
      sponsor_id: id,
    });
  }
  axios.get("https://shion1305.com/seiryo22/request?target=" + id);
}
</script>
<template>
  <swiper v-if="store.state.sponsors.length!==0" :autoplay="{
  delay: 4500,
  disableOnInteraction: false,
  }" :breakpoints="{
          430: {
          slidesPerView: 3,
          spaceBetween: 5,
          },
          800: {
          slidesPerView: 4,
          spaceBetween: 20,
          },

          }"
          :loop="true"
          :slidesPerGroup="2"
          :slidesPerView="2"
          :spaceBetween="10"
          class="sponsorsSwiper">

    <swiper-slide v-for="ad in randomList(store.state.sponsors)" :key="ad.id">
      <a :href="`${ad.url}`" rel="noopener noreferrer"
         target="_blank"
         v-on:click="access(`${ad.sponsor}`)"><img
          :src="`${ad.image.url}`" alt=""/></a>
    </swiper-slide>
  </swiper>
</template>

<style lang="scss">

.swiper {
  max-width: 50rem;
  width: 100vw;
  height: 100%;
}

.swiper-slide {
  text-align: center;
  font-size: 18px;
  background: #fff;

  /* Center slide text vertically */
  display: -webkit-box;
  display: -ms-flexbox;
  display: -webkit-flex;
  display: flex;
  -webkit-box-pack: center;
  -ms-flex-pack: center;
  -webkit-justify-content: center;
  justify-content: center;
  -webkit-box-align: center;
  -ms-flex-align: center;
  -webkit-align-items: center;
  align-items: center;
}

.swiper-slide img {
  display: block;
  width: 100%;
  height: 100%;
  object-fit: cover;
}
</style>