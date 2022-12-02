<template>
  <v-btn-toggle v-model="localOrder" density="compact" @click.prevent="change">
    <v-btn icon="mdi-pin" />
  </v-btn-toggle>
</template>

<script lang="ts" setup>
import { ref } from "vue";

const props = defineProps<{
  order: string;
}>();

const localOrder = ref(props.order);

const emit = defineEmits(["change:order"]);
const change = () => emit("change:order");
</script>
