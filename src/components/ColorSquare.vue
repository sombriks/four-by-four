<script setup>
import * as Tone from "tone";

const props = defineProps(["note"]);
const synth = new Tone.Synth().toDestination();

const makeSound = () => {
  synth.triggerAttackRelease(props.note, "8n");
};
</script>

<template>
  <button @click="makeSound"></button>
</template>

<style scoped></style>
