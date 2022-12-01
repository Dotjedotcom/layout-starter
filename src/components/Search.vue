<template>
  <v-card class="d-flex justify-center align-center">
    <h4>Zoek:</h4>
    <v-card-text>
      <v-text-field
          v-model="search"
          density="comfortable"
          variant="solo"
          label="Hup hup zoeken, klanten worden niet zelf gebeld.."
          append-inner-icon="mdi-magnify"
          single-line
          hide-details
      ></v-text-field>
    </v-card-text>
  </v-card>
</template>
<script lang="ts" setup>
  import {ref} from "vue";

  const search = ref('')
</script>
