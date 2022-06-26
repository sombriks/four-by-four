<script setup>
import { computed } from "vue";
import ColorSquare from "./ColorSquare.vue";

const props = defineProps(["size", "wh"]);

const tones = ["C", "D", "E", "F", "G", "A", "B"];

const makeNote = (m, n) => {
  return tones[m] + (n + 3);
};

const squares = computed(() => {
  let list = [];
  for (let i = 0; i < props.size; i++) {
    for (let j = 0; j < props.size; j++) {
      list.push(makeNote(i, j));
    }
  }
  return list;
});

const proportions = computed(() => {
  let pct = 100 / props.size;
  let i = props.size;
  let ret = "";
  while (i--) ret += `${pct}% `;
  return ret;
});
</script>

<template>
  <div class="pane">
    <div class="board">
      <ColorSquare v-for="s in squares" :key="s" :note="s" />
    </div>
  </div>
</template>

<style scoped>
.pane {
  display: flex;
  justify-content: center;
}
.board {
  width: v-bind(wh);
  height: v-bind(wh);
  display: grid;
  grid-template-columns: v-bind(proportions);
  grid-template-rows: v-bind(proportions);
}
</style>
