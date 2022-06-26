<script setup>
import * as Tone from "tone";
import { ref, computed } from "vue";
import GridBoard from "./components/GridBoard.vue";

const s = ref(4);
const started = ref(false);

const prepareSound = async () => {
  await Tone.start();
  started.value = true;
};

const wh = computed(
  () =>
    `${
      (window.innerWidth < window.innerHeight
        ? window.innerWidth
        : window.innerHeight) - 100
    }px`
);
</script>

<template>
  <div class="content">
    <h1>Four by Four</h1>
    <button class="big-start" v-if="!started" @click="prepareSound">Start</button>
    <GridBoard :size="s" :wh="wh" v-if="started" />
  </div>
</template>

<style>
:root {
  --bg-root: #9fc2cc;
  --bg-square: #1b5299;
  --fg-square: #f1ecce;
  --bg-active: #2b62a9;
  background-color: var(--bg-root);
}

button {
  background-color: var(--bg-square);
  color: var(--fg-square);
  border: none;
  margin: 1%;
  border-radius: 5%;
}

button:active {
  background-color: var(--bg-active);
}

.content {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.big-start {
  width: v-bind(wh);
  height: v-bind(wh);
  font-size: xx-large;
}
</style>
