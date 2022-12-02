<script setup lang="ts">
import { computed, nextTick, ref } from "vue";
import { useDateFormat, useTimestamp, useWebWorkerFn } from "@vueuse/core";
const heavyTask = () => {
  const randomNumber = () => Math.trunc(Math.random() * 5_000_00);
  const numbers: number[] = Array(5_000_000).fill(undefined).map(randomNumber);
  numbers.sort();
  return numbers.slice(0, 5);
};
const { workerFn, workerStatus, workerTerminate } = useWebWorkerFn(heavyTask);
const time = useTimestamp();
const computedTime = useDateFormat(time, "YYYY-MM-DD HH:mm:ss SSS");
const running = computed(() => workerStatus.value === "RUNNING");
const data = ref<number[] | null>(null);
const runner = ref("");
const baseSort = async () => {
  data.value = null;
  await nextTick();
  data.value = heavyTask();
  runner.value = "Main";
};
const workerSort = async () => {
  data.value = null;
  await nextTick();
  data.value = await workerFn();
  runner.value = "Worker";
};
</script>

<template>
  <v-card-title>
    Current Time: <b>{{ computedTime }}</b>
  </v-card-title>
  <v-card-item>
    This is a demo showing sort for large array (5 milion numbers) with or w/o
    WebWorker.<br />Clock stops when UI blocking happens.
  </v-card-item>
  <v-card-actions>
    <v-btn @click="baseSort"> Sort in Main Thread </v-btn>
    <v-btn v-if="!running" @click="workerSort"> Sort in Worker </v-btn>
    <v-btn v-else class="orange" @click="workerTerminate">
      Terminate Worker
    </v-btn>
  </v-card-actions>
  <v-card-text v-if="data">
    Thread: <strong>{{ runner }}</strong
    ><br />
    Result: <strong>{{ data }}</strong>
  </v-card-text>
</template>
