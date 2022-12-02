<template>
  <v-btn-group density="compact">
    <v-btn icon="mdi-play" :color="isActive ? 'red' : ''" @click="resume" />
    <v-btn icon="mdi-pause" :color="!isActive ? 'purple' : ''" @click="pause" />
    <v-btn icon="mdi-clock" />
    <v-btn>{{ time }}</v-btn>
  </v-btn-group>
</template>

<script lang="ts" setup>
import { ref } from "vue";
import { useIntervalFn } from "@vueuse/core";
import dayjs from "dayjs";

const time = ref("00:00:00");
const interval = ref(1000);
const { pause, resume, isActive } = useIntervalFn(
  () => (time.value = dayjs().format("hh:mm:ss")),
  interval
);
</script>
