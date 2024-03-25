<script setup lang="ts">
const configKonva = {
  width: 200,
  height: 200,
};
const configCircle = {
  x: 100,
  y: 100,
  radius: 70,
  fill: "red",
  stroke: "black",
  strokeWidth: 4,
};
</script>

<template>
  <v-stage :config="configKonva">
    <v-layer>
      <v-circle :config="configCircle"></v-circle>
    </v-layer>
  </v-stage>
</template>
