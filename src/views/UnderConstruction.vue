<script setup>
import {useMeta} from "vue-meta";
import {event} from "vue-gtag";

useMeta({
  title: "作成中...",
  description: "このページは作成中です!公開までしばらくお待ちください"
})

if (process.env.NODE_ENV === "production") {
  event("page:under_construction");
}
</script>
<template>
  <div class="content-frame fadeUp" style="animation-delay: 0.2s">
    <div class="fadeUp" style="animation-delay: 0.4s">
      <img alt="かもめ先輩、勉強中!" src="@/assets/kamome_sempai/writing.webp"/>
      <div style="font-size: 1.5rem">Under Construction...</div>
      <div id="not-found">このページは作成中です!<br>公開までしばらくお待ちください</div>
    </div>
  </div>
</template>


<style scoped>
#not-found {
  font-size: 1.2rem;
}

.content-frame {
  white-space: nowrap;
  width: min(100% - 2rem, 60rem);
  margin-inline: auto;
  display: flex;
  position: relative;
  text-align: center;
  background-size: cover;
  flex-direction: column;
  align-items: center;
  border-radius: 2rem;
  background-image: url("/public/image/image2.webp");
  margin-bottom: 1rem;
}

.content-frame img {
  background-size: contain;
  width: 100%;
  max-width: 300px;
}

.content-frame > div {
  width: fit-content;
  margin: 20px;
  background: #cd4fffcc;
  color: white;
  padding: 1rem 1.5rem;
  border-radius: 3rem;
}

@media screen and (max-width: 450px) {
  #not-found {
    font-size: 18px;
  }
}
</style>