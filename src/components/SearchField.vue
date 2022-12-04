<template>
  <v-card density="comfortable" class="d-flex justify-center align-center">
    <v-card-title class="pt-0 pl-0">Zoek:</v-card-title>
    <v-card-text>
      <v-text-field
        v-model="search"
        :loading="loading"
        :rules="[rules.required, rules.min]"
        density="comfortable"
        variant="solo"
        label="Hup hup zoeken, klanten worden niet zelf gebeld.."
        append-inner-icon="mdi-magnify"
        single-line
        hide-details="auto"
        @keyup="keyup"
        @keydown.enter="click"
        @click:append-inner="click"
      ></v-text-field>
    </v-card-text>
  </v-card>
</template>

<script lang="ts" setup>
import { reactive, ref } from "vue";

const search = ref("");
const loading = ref(false);
const loaded = ref(false);
const emit = defineEmits<{
  (e: "update:search", str: string): void;
}>();
const keyup = () => emit("update:search", search.value);
const click = () => {
  loading.value = true;
  setTimeout(() => {
    loading.value = false;
    loaded.value = true;
    emit("update:search", search.value);
  }, 2000);
};

const rules = reactive({
  required: (value: string) => !!value ?? "Verplicht.",
  min: (value: string) =>
    (value && value.length >= 3) || "Mininmaal 3 karakters",
});
</script>
