<script setup lang="ts">
import { onMounted, ref, watch } from "vue";
import { useSpeechSynthesis } from "@vueuse/core";
const voice = ref<SpeechSynthesisVoice>(
  undefined as unknown as SpeechSynthesisVoice
);
const props = defineProps<{
  search: string;
}>();
console.log("props", props.search);
// const emit = defineEmits(["change:darkmode"]);
// const change = () => emit("change:darkmode");
const text = ref(props.search ?? "Hallo, ik ben jan en 47 jaar oud.");
const speech = useSpeechSynthesis(text, { voice });
const voices = ref<SpeechSynthesisVoice[]>([]);
let synth: SpeechSynthesis;
watch(
  () => props.search,
  () => (text.value = props.search)
);
onMounted(() => {
  if (speech.isSupported.value) {
    // load at last
    setTimeout(() => {
      synth = window.speechSynthesis;
      voices.value = synth.getVoices();
      voice.value = voices.value[0];
    });
  }
});
const play = () =>
  speech.status.value === "pause"
    ? window.speechSynthesis.resume()
    : speech.speak();
const pause = () => {
  window.speechSynthesis.pause();
};
const stop = () => {
  window.speechSynthesis.cancel();
};
</script>

<template>
  <v-card>
    <v-card-text>
      Search: {{ search }} Text: {{ text }}
      <div v-if="!speech.isSupported">
        Your browser does not support SpeechSynthesis API,
        <a
          href="https://caniuse.com/mdn-api_speechsynthesis"
          rel="noreferrer noopener"
          target="_blank"
          >more details</a
        >
      </div>
      <div v-else>
        <v-input
          v-model="text"
          label="Spoken Text"
          class="!inline-block"
          type="text"
        />

        <br />
        <!--        {{ voice.name }} {{ voice.lang }} -->
        <!--        {{ voices.forEach((i) => `${i.name} ${i.lang}`) }} -->
        <!--        <v-select -->
        <!--          v-model="voice" -->
        <!--          :items="voices" -->
        <!--          :item-title="voice.name" -->
        <!--          label="Language" -->
        <!--          persistent-hint -->
        <!--          return-object -->
        <!--          single-line -->
        <!--        /> -->

        <div class="d-sm-flex">
          <select v-model="voice">
            <option disabled>Select Language</option>
            <option v-for="(voice, i) in voices" :key="i" :value="voice">
              {{ `${voice.name} (${voice.lang})` }}
            </option>
          </select>
        </div>

        <div class="mt-2">
          <v-btn :disabled="speech.isPlaying.value" @click="play">
            {{ speech.status.value === "pause" ? "Resume" : "Speak" }}
          </v-btn>
          <v-btn
            :disabled="!speech.isPlaying.value"
            class="orange"
            @click="pause"
          >
            Pause
          </v-btn>
          <v-btn :disabled="!speech.isPlaying.value" class="red" @click="stop">
            Stop
          </v-btn>
        </div>
      </div>
    </v-card-text>
  </v-card>
</template>
