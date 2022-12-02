<template>
  <v-card color="green">
    <v-card-title>DevTools BOOM 💥</v-card-title>
    <v-card v-if="false" color="white">
      <WebWorkerDemo />
    </v-card>
    <v-card color="green">
      <v-card-title>Logging</v-card-title>
      <v-card-text>{{ props.log }}</v-card-text>
    </v-card>
  </v-card>
</template>

<script lang="ts" setup>
import WebWorkerDemo from "@/components/WebWorkerDemo.vue";
const props = defineProps<{
  log: string;
}>();
</script>
