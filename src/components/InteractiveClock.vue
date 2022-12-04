<template>
  <v-btn-group density="compact">
    <v-btn icon="mdi-play" :color="isActive ? 'red' : ''" @click="resume" />
    <v-btn icon="mdi-pause" :color="!isActive ? 'purple' : ''" @click="pause" />
    <v-btn icon="mdi-clock" />
    <v-btn>{{ time }}</v-btn>
    <v-btn icon="mdi-minus" @click="add(-10)"></v-btn>
    <v-btn>{{ output.toFixed(2).padStart(5, "0") }}</v-btn>
    <v-btn icon="mdi-plus" @click="add(10)"></v-btn>
  </v-btn-group>
</template>

<script lang="ts" setup>
import { TransitionPresets, useIntervalFn } from "@vueuse/core";
import { ref } from "vue";
import { useTransition } from "@vueuse/core";
import dayjs from "dayjs";

const time = ref("00:00:00");
const interval = ref(1000);
const source = ref(0);
const add = (num: number) => (source.value += num);

const { pause, resume, isActive } = useIntervalFn(
  () => (time.value = dayjs().format("hh:mm:ss")),
  interval
);

const output = useTransition(source, {
  duration: 1000,
  transition: TransitionPresets.easeInOutCubic,
});
</script>
