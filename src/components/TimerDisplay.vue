<template>
  <v-card class="ma-2 pa-4">
    <v-card-title>Counter</v-card-title>
    <v-card-text>
      <v-banner> now: {{ now }} </v-banner>
      <v-btn @click="pause">Pause</v-btn>
      <v-btn @click="resume">Resume</v-btn>
    </v-card-text>
    <v-card-text>
      <v-banner> timestamp: {{ timestamp }} </v-banner>
      <v-btn @click="pauseT">Pause</v-btn>
      <v-btn @click="resumeT">Resume</v-btn>
    </v-card-text>
  </v-card>
</template>

<script lang="ts" setup>
import { useNow, useTimestamp } from "@vueuse/core";

const { now, pause, resume } = useNow({ controls: true });

const {
  timestamp,
  pause: pauseT,
  resume: resumeT,
} = useTimestamp({ controls: true });
</script>

<style scoped></style>
