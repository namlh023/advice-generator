<script setup>
import axios from "axios";
import { reactive, watchEffect } from "vue";
import diviceImage from "./assets/images/pattern-divider-mobile.svg";
import iconDice from "./assets/images/icon-dice.svg";

const advice = reactive({
  id: 0,
  content: "",
});
const getAdvice = async () => {
  try {
    const {
      data: { slip },
    } = await axios.get("https://api.adviceslip.com/advice");
    advice.id = slip.id;
    advice.content = slip.advice;
  } catch {
    advice.content = "This is the way";
  }
};
watchEffect(getAdvice);
</script>
<template>
  <main class="main">
    <div class="advice-card">
      <span class="advice-id">ADVICE #{{ advice.id }}</span>
      <p class="content">
        {{ advice.content }}
      </p>
      <div class="divider">
        <img :src="diviceImage" />
      </div>
      <button class="generate" @click="getAdvice">
        <img :src="iconDice" />
      </button>
    </div>
  </main>
</template>
<style lang="scss" scoped>
@import "./style.scss";
.main {
  min-width: 100vw;
  min-height: 100vh;
  background-color: $darkBlue;
  display: flex;
  align-items: center;
  justify-content: center;

  .advice-card {
    background-color: $darkGreyishBlue;
    width: 400px;
    padding: 16px;
    padding-bottom: 40px;
    box-shadow: 30px 50px 80px rgba(0, 0, 0, 0.100202);
    border-radius: 15px;
    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction: column;
    position: relative;

    .advice-id {
      font-family: "Manrope";
      color: $neonGreen;
      font-weight: 800;
      font-size: 10px;
      line-height: 16px;
      letter-spacing: 4.08571px;
      text-align: center;
    }

    .content {
      font-family: "Manrope";
      font-weight: 800;
      font-size: 20px;
      line-height: 30px;
      text-align: center;
      color: $lightCyan;
      min-height: 100px;
      display: flex;
      justify-content: center;
      align-items: center;
    }

    .generate {
      background-color: $neonGreen;
      padding: 12px;
      border-radius: 50%;
      display: flex;
      justify-content: center;
      align-items: center;
      position: absolute;
      bottom: -25px;
      cursor: pointer;
      border: none;
    }
  }
}
</style>
