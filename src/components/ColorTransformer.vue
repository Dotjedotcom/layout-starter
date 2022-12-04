<template>
  <v-card class="d-flex justify-center align-center">
    <v-card-title>Color</v-card-title>
    <v-card-text>
      <div
        class="fixed-width pa-4"
        :class="classText"
        :style="{ 'background-color': `${color}` }"
      >
        {{ color }} {{ isDark() }} {{ classText }}
      </div>
    </v-card-text>
    <v-card-text>
      <div class="d-flex">
        <v-slider
          v-model="r"
          label="Red"
          :step="1"
          :min="min"
          :max="max"
        ></v-slider>
        <v-slider
          v-model="g"
          label="Green"
          :step="1"
          :min="min"
          :max="max"
        ></v-slider>
        <v-slider
          v-model="b"
          label="Blue"
          :step="1"
          :min="min"
          :max="max"
        ></v-slider>
        <v-slider
          v-model="a"
          label="Alpha"
          :step="0.1"
          :min="min"
          :max="max"
        ></v-slider>
      </div>
    </v-card-text>
  </v-card>
</template>

<script lang="ts" setup>
import { computed, reactive, ref } from "vue";
import { reactify, useTransition } from "@vueuse/core";
const min = 0,
  max = 255,
  mid = max / 2;
const classText = ref("text-white");
const isDark = reactify(() => {
  return source.some((color) => color.value < mid) &&
    (r.value < mid || g.value < mid || b.value < mid)
    ? (classText.value = "text-white")
    : (classText.value = "text-black");
});

const r = ref(Math.ceil(0)),
  g = ref(70),
  b = ref(200),
  a = ref(1);
const source = reactive([r, g, b]);
const output = useTransition(source);
const color = computed(() => {
  const [r, g, b] = output.value;
  return `rgba(${Math.ceil(r)}, ${Math.ceil(g)}, ${Math.ceil(b)}, ${a.value})`;
});
</script>

<style scoped>
.fixed-width {
  width: 200px;
}
</style>
