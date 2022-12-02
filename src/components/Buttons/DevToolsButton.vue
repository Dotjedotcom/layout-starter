<template>
  <v-tooltip text="DevTools" location="bottom">
    <template #activator="{ props }">
      <v-btn
        rounded
        v-bind="props"
        :icon="prop.bar ? 'mdi-lock-open' : 'mdi-lock'"
        @click="change"
      />
    </template>
  </v-tooltip>
</template>

<script lang="ts" setup>
const prop = defineProps<{
  bar: boolean;
}>();

const emit = defineEmits("update:bar");
const change = () => emit("update:bar");
</script>
