<template>
  <v-tooltip
    :text="`Dark-mode: ${prop.theme === 'dark' ? 'aan' : 'uit'}`"
    location="bottom"
    ><template #activator="{ props }">
      <v-btn
        :icon="
          prop.theme === 'light' ? 'mdi-weather-sunny' : 'mdi-weather-night'
        "
        v-bind="props"
        rounded
        @click="change"
    /></template>
  </v-tooltip>
</template>

<script lang="ts" setup>
const prop = defineProps<{
  theme: string;
}>();
const emit = defineEmits(["change:darkmode"]);
const change = () => emit("change:darkmode");
</script>
