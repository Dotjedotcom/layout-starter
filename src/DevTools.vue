<template>
  <v-card color="green">
    <v-card-title>DevTools BOOM 💥</v-card-title>
    <v-card color="white">
      <WebWorkerDemo/>
    </v-card>
    <v-card color="green">
      <v-card-title>Logging</v-card-title>
      <v-card-text>{{ log }}</v-card-text>
    </v-card>
  </v-card>
</template>

<script lang="ts" setup>
import WebWorkerDemo from '@/components/WebWorkerDemo';
const props = defineProps({ log: String })
</script>
