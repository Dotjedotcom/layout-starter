<template>
  <v-app :theme="theme">
    <v-layout>
      <v-navigation-drawer
        v-model="drawer"
        elevation="2"
        :rail="rail"
        permanent
        @click="rail = false"
      >
        <v-list-item
          prepend-avatar="https://randomuser.me/api/portraits/men/86.jpg"
          title="Janushki Dotingolaev von Ravensburger tot Bruhckensthein"
          nav
        >
          <template #append>
            <v-btn
              variant="text"
              icon="mdi-chevron-left"
              @click.stop="rail = !rail"
            ></v-btn>
          </template>
        </v-list-item>

        <v-divider />

        <v-list density="compact" nav>
          <v-list-item
            prepend-icon="mdi-home-city"
            title="Home"
            value="home"
          ></v-list-item>
          <v-list-item
            prepend-icon="mdi-account"
            title="My Account"
            value="account"
          ></v-list-item>
          <v-list-item
            prepend-icon="mdi-account-group-outline"
            title="Users"
            value="users"
          ></v-list-item>
        </v-list>
      </v-navigation-drawer>

      <v-navigation-drawer
        v-if="extraBar"
        width="500"
        color="grey-darken-1"
        permanent
      >
        <DevTools :log="search" />
      </v-navigation-drawer>

      <v-app-bar height="56" color="grey" elevation="0">
        <template #prepend><Clock /></template>

        <template #append>
          <v-btn icon="mdi-heart"></v-btn>
          <BarOrderButton :order="barOrder" @change:order="changeOrder" />
        </template>
      </v-app-bar>

      <v-navigation-drawer
        v-model="drawer"
        location="right"
        elevation="2"
        :rail="railRight"
        permanent
        expand-on-hover
        @click="railRight = false"
      >
        <v-list-item title="Opnemen" nav>
          <template #prepend>
            <v-btn icon="mdi-phone" elevation="0"></v-btn>
          </template>
          <template #append>
            <v-btn
              variant="text"
              icon="mdi-chevron-left"
              @click.stop="railRight = !railRight"
            ></v-btn>
          </template>
        </v-list-item>

        <v-divider></v-divider>

        <v-list density="compact" nav>
          <v-list-item
            prepend-icon="mdi-home-city"
            title="Home"
            value="home"
          ></v-list-item>
          <v-list-item
            prepend-icon="mdi-account"
            title="My Account"
            value="account"
          ></v-list-item>
          <v-list-item
            prepend-icon="mdi-account-group-outline"
            title="Users"
            value="users"
          ></v-list-item>
        </v-list>
      </v-navigation-drawer>

      <v-app-bar
        height="56"
        color="grey-lighten-2"
        elevation="2"
        :order="barOrder"
      >
        <template #prepend>
          <v-btn icon="mdi-hamburger"></v-btn>
          <h3>Vue 3 and Vuetify 3...</h3>
        </template>

        <template #append>
          <DarkModeButton :theme="theme" @change:darkmode="changeDarkmode" />
          <DevToolsButton :bar="extraBar" @update:bar="toggleBar" />
          <Settings />
          <!--          <v-btn icon="mdi-dots-vertical"></v-btn> -->
        </template>
      </v-app-bar>

      <v-app-bar
        location="bottom"
        height="48"
        color="grey-lighten-2"
        elevation="0"
      >
        <v-tooltip text="Tooltip">
          <template #activator="{ props }">
            <p class="pa-4">&copy; DotjeDotCom Productions 🌈</p>
            <v-btn v-bind="props">Tooltip</v-btn>
          </template>
        </v-tooltip>
      </v-app-bar>

      <v-main>
        <SearchField class="ma-2 pa-4" @update:search="updateSearch" />
        <SpeechSynthesis :search="search" />
        <TimerDisplay />
        <ColorTransformer />
        <v-card class="ma-2 pa-4">
          <HelloWorld />
        </v-card>
      </v-main>
    </v-layout>
  </v-app>
</template>

<script lang="ts" setup>
import { ref } from "vue";
import BarOrderButton from "@/components/Buttons/BarOrderButton.vue";
import Clock from "@/components/InteractiveClock.vue";
import ColorTransformer from "@/components/ColorTransformer.vue";
import DarkModeButton from "@/components/Buttons/DarkModeButton.vue";
import DevTools from "@/components/DevTools.vue";
import DevToolsButton from "@/components/Buttons/DevToolsButton.vue";
import HelloWorld from "@/components/HelloWorld.vue";
import SearchField from "@/components/SearchField.vue";
import Settings from "@/components/SettingsDialog.vue";
import SpeechSynthesis from "@/components/SpeechSynthesis.vue";
import TimerDisplay from "@/components/TimerDisplay.vue";

const changeOrder = () =>
  (barOrder.value = barOrder.value === "0" ? "-1" : "0");
const changeDarkmode = () =>
  (theme.value = theme.value === "light" ? "dark" : "light");
const toggleBar = () => (extraBar.value = !extraBar.value);
const updateSearch = (newValue: string) => (search.value = newValue);

const barOrder = ref("-1");
const drawer = ref(true);
const extraBar = ref(false);
const rail = ref(true);
const railRight = ref(true);
const theme = ref("light");
const search = ref("");
</script>
