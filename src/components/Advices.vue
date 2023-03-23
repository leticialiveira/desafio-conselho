<script setup>
import axios from "axios";
import { ref } from "vue";
import Loading from "./Loading.vue";

const text = ref("???");
const loading = ref(false);

function ButtonAdvice() {
  loading.value = true
  axios
    .get("https://api.adviceslip.com/advice")
    .then((res) => {
      loading.value =false
      text.value = res.data.slip.advice;
    })
    .catch((error) => {
      console.log(error);
    });
}
</script>

<template>
  <div class="main">
    <h1>Want to receive some advice?</h1>
    <button @click="ButtonAdvice">advices</button>
    <p class="response" v-show="!loading">{{ text }}</p>
    <Loading v-show="loading" />
  </div>
</template>

<style scoped>
.main {
  background: linear-gradient(
    90deg,
    rgba(2, 0, 36, 1) 0%,
    rgba(9, 9, 121, 1) 18%,
    rgba(0, 212, 255, 1) 87%
  );
  width: 700px;
  height: 500px;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  gap: 50px;
}

.main p {
  font-style: normal;
  font-weight: 700;
  line-height: 72px;
  color: #D6D6D6;
  width: 500px;
  margin: 0;
}
</style>
