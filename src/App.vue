<template>
  <div class="view">
    <main-screen
      v-if="statusMatch === 'default'"
      @onStart="onHandleBeforeStart($event)"
    />
    <interact-screen
      v-if="statusMatch === 'match'"
      :cardsContext="settings.cardsContext"
      @onFinish="onGetResult"
    />
    <result-screen
      v-if="statusMatch === 'result'"
      :timer="timer"
      @restartGame="onRestart"
    />
    <copy-right-screen />
  </div>
</template>
<script>
import MainScreen from "./components/MainScreen.vue";
import CopyRightScreen from "./components/CopyRightScreen.vue";
import InteractScreen from "./components/InteractScreen.vue";
import ResultScreen from "./components/ResultScreen.vue";
import { shuffled } from "../src/utils/array.js";

export default {
  name: "App",
  data() {
    return {
      settings: {
        totalOfBlock: 0,
        cardsContext: [],
        startedAt: null,
      },
      statusMatch: "default",
      timer: 0,
    };
  },
  components: {
    MainScreen,
    CopyRightScreen,
    InteractScreen,
    ResultScreen,
  },
  methods: {
    onHandleBeforeStart(config) {
      this.settings.totalOfBlock = config.totalOfBlock;

      const firstCards = Array.from(
        { length: this.settings.totalOfBlock / 2 },
        (_, i) => i + 1
      );
      const cards = [...firstCards, ...firstCards];
      this.settings.cardsContext = shuffled(
        shuffled(shuffled(shuffled(cards)))
      );
      console.log(this.settings.cardsContext);
      this.settings.startedAt = new Date().getTime();
      this.statusMatch = "match";
    },
    onGetResult() {
      //get timer
      this.timer = new Date().getTime() - this.settings.startedAt;

      //switch screen
      this.statusMatch = "result";
    },

    onRestart() {
      this.statusMatch = "default";
    },
  },
};
</script>
