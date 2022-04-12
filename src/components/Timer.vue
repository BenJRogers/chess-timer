<template >
  <div @click.prevent="timerClicked()">
    <div
      class="timer"
      :class="{
        active: this.isActive,
        timedOut: timedOut,
      }"
    >
      <p>{{ formatTime }}</p>
      <p class="timer-count">Moves: {{ timerCount }}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: "Timer",
  props: ["time", "player"],
  emits: ["timer_created", "timerClicked"],
  methods: {
    timerClicked() {
      this.$emit("timerClicked", this.player);
    },
    startTimer() {
      this.intervalTimer = setInterval(this.trackTime, 1000);
    },
    stopTimer() {
      clearInterval(this.intervalTimer);
    },
    trackTime() {
      setTimeout(() => {
        this.timeTracker !== 1 ? this.reduceTime() : this.timeTracker--
      }, 1);
    },
    reduceTime() {
      this.timeTracker = 1000;
      if (this.timerAmount === 1) {
        this.timedOut = true;
      }
      if (this.timerAmount > 0) {
        this.timerAmount--;
      } else {
        this.stopTimer();
      }
    },
    resetTimer() {
      this.timerCount = 0;
    },
  },

  computed: {
    formatTime() {
      let formatedSeconds = this.timerAmount;

      let hours = Math.floor(this.timerAmount / 3600);
      formatedSeconds %= 3600;
      let minutes = Math.floor(formatedSeconds / 60);
      let seconds = formatedSeconds % 60;

      return `${hours > 0 ? hours + ":" : ""}${minutes}:${seconds < 10 ? "0" : ""
        }${seconds}`;
    },
  },
  data() {
    return {
      isActive: false,
      timerAmount: this.time,
      intervalTimer: null,
      timedOut: false,
      timerCount: 0,
      timeTracker: 1000,
    };
  },
  created() {
    this.$emit("timer_created", this);
  },
};
</script>

<style scoped>
.timer {
  border: 1px solid black;
  border-radius: 20px;
  width: 320px;
  height: 100%;
  background-color: #5d5d5d;
  display: flex;
  flex-direction: column;
  align-items: center;
  cursor: pointer;
}
.active {
  /* background-color: #86c322; */
  background-color: #8eb33b;
}
.timedOut {
  /* background-color: #c75646; */
  background-color: #c75646;
}
p {
  color: white;
  font-size: 100px;
  margin: 25px 0;
}
.timer-count {
  font-size: 22px;
  margin: 0;
  display: flex;
  align-self: flex-end;
  margin-right: 18px;
}
</style>
