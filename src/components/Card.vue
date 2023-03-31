<template>
  <div
    class="card"
    :class="{ disable: isDisable }"
    :style="{
      height: `${(850 - 32 * 2) / Math.sqrt(cardContext.length) - 16}px`,
      width: `${
        (((850 - 32 * 2) / Math.sqrt(cardContext.length) - 16) * 3) / 4
      }px`,
      perspective: `${
        ((((850 - 32 * 2) / Math.sqrt(cardContext.length) - 16) * 3) / 4) * 1.8
      }px`,
    }"
  >
    <div
      class="card__inner"
      :class="{ 'is-fliped': isFliped }"
      @click="onToggleClick"
    >
      <div class="card__face card__face--front">
        <div class="card__content"></div>
      </div>
      <div class="card__face card__face--back">
        <div
          class="card__content"
          :style="{
            'background-image': `url(${require('@/assets/' + imgUrl)})`,
          }"
        ></div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  props: {
    imgUrl: {
      type: String,
      required: true,
    },
    card: {
      type: [Number, String, Array, Object],
      required: true,
    },
    rules: {
      type: Array,
    },
    cardContext: {
      type: Array,
      default: function () {
        return [];
      },
    },
  },
  data() {
    return {
      isFliped: false,
      isDisable: false,
      countClick: 0,
    };
  },
  methods: {
    onFlipBackCard() {
      this.isFliped = false;
      this.countClick = 0;
    },

    onToggleClick() {
      if (this.countClick < 2) this.countClick++;
      if (this.countClick >= 2) return;
      if (this.rules.length >= 2) {
        this.countClick = 0;
        return;
      }
      if (this.isDisable === true) return false;
      this.isFliped = !this.isFliped;
      if (this.isFliped) this.$emit("onFlip", this.card);
    },

    onEnableMode() {
      this.isDisable = true;
    },
  },
};
</script>
<style lang="css">
.card {
  display: inline-block;
  margin-right: 1rem;
  margin-bottom: 1rem;
}

.card.disable .card__inner {
  cursor: no-drop;
}

.card__inner {
  width: 100%;
  height: 100%;
  position: relative;
  transition: transform 1s;
  transform-style: preserve-3d;
  cursor: pointer;
}

.card__inner.is-fliped {
  transform: rotateY(-180deg);
}

.card__face {
  position: absolute;
  width: 100%;
  height: 100%;
  backface-visibility: hidden;
  overflow: hidden;
  border: 1px solid #ffbb00;
  border-radius: 10px;
  padding: 10px;
  box-shadow: 0 3px 10px 3px rgba(0, 0, 0, 0.2);
}

.card__face--front {
  background: #110023;
}

.card__face--front .card__content {
  background: url("../assets/images/icon_back.png") no-repeat center center;
  background-size: 70%;
  width: 100%;
  height: 100%;
}

.card__face--back {
  transform: rotateY(-180deg);
  background: var(--light);
}

.card__face--back .card__content {
  width: 100%;
  height: 100%;
  background-position: center center;
  background-size: 90%;
  background-repeat: no-repeat;
}
</style>
