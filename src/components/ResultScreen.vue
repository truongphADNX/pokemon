<template>
  <div class="result-screen">
    <h1 class="result__title">YOU ARE WINNER</h1>
    <span class="result__desc">Timer:{{ Math.round(timer / 1000) }} </span>
    <button class="result__btn" @click="restart">Restart</button>
  </div>
</template>
<script>
export default {
  props: {
    timer: {
      type: Number,
      default: 0,
    },
  },
  methods: {
    restart() {
      this.$emit("restartGame");
    },
  },
};
</script>
<style scoped lang="css">
.result-screen {
  height: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 30px;
}

.result__title {
  font-size: 5.4rem;
  font-weight: 700;
  background: radial-gradient(
    circle,
    rgb(231, 247, 0) 0%,
    rgba(252, 70, 107, 1) 100%
  );
  background-clip: text;
  -webkit-background-clip: text;
  color: #131313;
  text-shadow: 0 -1px 4px #fff, 0 -2px 10px rgb(255, 184, 31),
    0 -10px 20px #8a1d1d, 0 -18px 40px #f00;
}
.result__desc {
  font-size: 5.4rem;
  font-weight: 700;
  background: radial-gradient(
    circle,
    rgb(231, 247, 0) 0%,
    rgba(252, 70, 107, 1) 100%
  );
  background-clip: text;
  -webkit-background-clip: text;
  color: #131313;
  text-shadow: 0 -1px 4px #fff, 0 -2px 10px rgb(255, 0, 119),
    0 -10px 20px #07fe0f, 0 -18px 40px rgb(98, 0, 227);
}

.result__btn {
  font-size: 1.8rem;
  padding: 5px;
  width: 100px;
  max-width: 100%;
  height: 50px;
  color: rgb(255, 255, 255);
  background: #4c00ff;
  text-align: center;
  border-radius: 5px;
  cursor: pointer;
}
</style>
