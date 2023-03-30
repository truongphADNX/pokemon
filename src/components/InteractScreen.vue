<template lang="html">
  <div class="screen">
    <card-flip
      v-for="(card, index) in cardsContext"
      :key="index"
      :ref="`card-${index}`"
      :imgUrl="`images/${card}.png`"
      :card="{ index: index, value: card }"
      @onFlip="checkRule($event)"
    />
  </div>
</template>
<script>
import CardFlip from "./Card";
export default {
  components: {
    CardFlip,
  },
  props: {
    cardsContext: {
      type: Array,
      default: function () {
        return [];
      },
    },
  },
  data() {
    return {
      rules: [],
    };
  },
  methods: {
    checkRule(card) {
      if (this.rules.length === 2) return false;
      this.rules.push(card);
      if (
        this.rules.length === 2 &&
        this.rules[0].value === this.rules[1].value
      ) {
        this.$refs[`card-${this.rules[0].index}`][0].onEnableMode();
        this.$refs[`card-${this.rules[1].index}`][0].onEnableMode();
        this.rules = [];
        const disableElements = document.querySelectorAll(
          ".screen .card.disable"
        );
        if (disableElements.length === this.cardsContext.length - 2) {
          setTimeout(() => {
            this.$emit("onFinish");
          }, 920);
        }
      } else if (
        this.rules.length === 2 &&
        this.rules[0].value !== this.rules[1].value
      ) {
        setTimeout(() => {
          this.$refs[`card-${this.rules[0].index}`][0].onFlipBackCard();
          this.$refs[`card-${this.rules[1].index}`][0].onFlipBackCard();
          this.rules = [];
        }, 800);
      } else {
        return false;
      }
    },
  },
};
</script>
