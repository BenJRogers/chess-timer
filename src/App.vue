<template>
  <div class="parent-container">
    <Settings
      v-if="showSettings"
      @close-settings="showSettings = !showSettings"
    />
    <div class="timer-container">
      <Timer
        :time="time"
        player="player1"
        @timer-clicked="setActivePlayer"
        @timer_created="registerTimer"
      />
      <div class="icon-container">
        <font-awesome-icon
          @click.prevent="(showSettings = !showSettings), stopTimer()"
          icon="ellipsis-h"
        />

        <font-awesome-icon
          @click.prevent="stopTimer"
          :class="{ pause: !running }"
          icon="pause"
        />
        <font-awesome-icon @click.prevent="reset" icon="undo" />
      </div>

      <Timer
        :time="time"
        player="player2"
        @timer-clicked="setActivePlayer"
        @timer_created="registerTimer"
      />
    </div>
  </div>
</template>

<script>
import Timer from "./components/Timer.vue";
import Settings from "./components/Settings.vue";

export default {
  name: "App",
  components: {
    Timer,
    Settings,
  },

  data() {
    return {
      time: 300,
      timers: {},
      activePlayer: null,
      inactivePlayer: null,
    };
  },
  watch: {
    activePlayer(newVal, oldVal) {
      if (oldVal && newVal !== oldVal) {
        this.timers[newVal].isActive = true;
        this.timers[oldVal].isActive = false;
        this.inactivePlayer = oldVal;
        this.startTimer();
      } else {
        this.timers[newVal].isActive = true;
        this.startTimer();
      }
    },
  },

  methods: {
    registerTimer(timerInstance) {
      this.timers[timerInstance.player] = timerInstance;
    },
    setActivePlayer(player) {
      this.activePlayer = player;
    },
    startTimer() {
      this.timers[this.activePlayer].startTimer();
      if (this.timers[this.inactivePlayer]) {
        this.timers[this.inactivePlayer].stopTimer();
      }
    },

    reset() {
      let confirmAction = confirm("Are you sure to execute this action?");
      if (confirmAction) {
        // this.stopTimer(true);
      } else {
        alert("Action canceled");
      }
    },
  },
};
</script>

<style>
body {
  background-color: #242424;
  color: #f7f7f7;
  font-family: "Manrope", sans-serif;
}
.parent-container {
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
}

.icon-container {
  font-size: 30px;
  color: #f7f7f7;
  display: flex;
  justify-content: space-evenly;
  padding: 25px 0;
}
.icon-container {
  cursor: pointer;
}
.pause {
  visibility: hidden;
}
</style>
