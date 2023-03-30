<template lang="html">
  <section class="screen">
    <h1 class="screen__title">POKE MEMORIES</h1>
    <h3 class="screen__desc">Select mode to start game</h3>
    <div class="actions">
      <button class="actions__item" @click="onStart(16)">
        <span class="actions__item--value">4x4</span>
        <span class="actions__item--desc">EASY</span>
      </button>
      <button class="actions__item" @click="onStart(36)">
        <span class="actions__item--value">6x6</span>
        <span class="actions__item--desc">MEDIUM</span>
      </button>
      <button class="actions__item" @click="onStart(64)">
        <span class="actions__item--value">8x8</span>
        <span class="actions__item--desc">HARD</span>
      </button>
      <button class="actions__item" @click="onStart(100)">
        <span class="actions__item--value">10x10</span>
        <span class="actions__item--desc">BRUTAL</span>
      </button>
    </div>
  </section>
</template>
<script>
export default {
  name: "MainScreen",
  methods: {
    onStart(totalOfBlock) {
      this.$emit("onStart", { totalOfBlock });
    },
  },
};
</script>
<style scoped lang="css">
.screen {
  background: #16dcfe;
  height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

.screen__title {
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
  text-shadow: 0 -1px 4px #fff, 0 -2px 10px #ff0, 0 -10px 20px #ff8000,
    0 -18px 40px #f00;
}
.screen__desc {
  margin-top: 60px;
  font-size: 28px;
}
.actions {
  margin-top: 20px;
  display: flex;
  gap: 10px;
}
.actions__item {
  padding: 5px;
  width: 100px;
  max-width: 100%;
  height: 50px;
  color: rgb(255, 255, 255);
  background: #7b00ff;
  display: flex;
  flex-direction: column;
  cursor: pointer;
}
.actions__item--value,
.actions__item--desc {
  margin: auto;
  font-weight: 500;
}
</style>
