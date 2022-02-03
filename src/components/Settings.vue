<template >
  <div class="lightbox">
    <span>
      <div class="settings-container">
        <font-awesome-icon
          class="close-icon"
          @click.prevent="$emit('close-settings')"
          icon="window-close"
        />
        <p>Timer 1</p>
        <input type="number" v-model.number="age" />
        <font-awesome-icon
          icon="link"
          @click.prevent="linkActive = !linkActive"
          :class="{ linkActive: linkActive }"
          class="link"
        />
        <p>Timer 2</p>
        <input type="number" v-model.number="age" />
      </div>
    </span>
  </div>
</template>

<script>
export default {
  emits: ["close-settings"],
  data() {
    return {
      linkActive: true,
    };
  },
};
</script>

<style scoped>
body {
  background-color: white;
  width: 200px;
  height: 200px;
  max-height: 50vh;
}
p {
  color: white;
  font-weight: bold;
}
.lightbox {
  /* Overlay entire screen */
  position: fixed;
  z-index: 999;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;

  /* A bit of padding around image */
  padding: 1em;

  /* Translucent background */
  background: rgba(0, 0, 0, 0.8);
}

/* Unhide the lightbox when it's the target */
.lightbox-display {
  display: block;
}

.lightbox span {
  /* Full width and height */
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  height: 100%;

  /* Size and position background image */
  background-position: center;
  background-repeat: no-repeat;
  background-size: contain;
}
.settings-container {
  width: 400px;
  height: 400px;
  padding: 15px;
  background-color: #474b4f;
  display: flex;
  align-content: center;
  flex-direction: column;
  margin: 50px;
}

.close-icon {
  color: #86c232;
  font-size: 30px;
  align-self: flex-end;
}
.link {
  font-size: 30px;
  align-self: flex-end;
  margin-top: 40px;
}
.linkActive {
  color: #86c232;
}
</style>