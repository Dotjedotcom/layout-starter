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
          <template v-slot:append>
            <v-btn
              variant="text"
              icon="mdi-chevron-left"
              @click.stop="rail = !rail"
            ></v-btn>
          </template>
        </v-list-item>

        <v-divider></v-divider>

        <v-list density="compact" nav>
          <v-list-item prepend-icon="mdi-home-city" title="Home" value="home"></v-list-item>
          <v-list-item prepend-icon="mdi-account" title="My Account" value="account"></v-list-item>
          <v-list-item prepend-icon="mdi-account-group-outline" title="Users" value="users"></v-list-item>
        </v-list>
      </v-navigation-drawer>

      <v-navigation-drawer v-if="extraBar" width="500" color="grey-darken-1" permanent>
        <DevTools />
      </v-navigation-drawer>

      <v-app-bar height="56" color="grey" elevation="0" >
        <template v-slot:prepend>
          <Clock/>
        </template>
        <template v-slot:append>
          <v-btn-toggle
            v-model="order"
            @click="changeOrder"
            dark
            rounded
            density="compact"
          >
            <v-btn>
              <v-icon>mdi-pin</v-icon>
            </v-btn>
          </v-btn-toggle>
          <v-btn icon="mdi-heart"></v-btn>
          <span class="pa-4">{{ `<< insert your logo here >>` }}</span>
        </template>
      </v-app-bar>

      <v-navigation-drawer location="right"
        v-model="drawer"
        elevation="2"
        :rail="railRight"
        permanent
        expand-on-hover
        @click="railRight = false"
      >
        <v-list-item
          title="Opnemen"
          nav
        >
          <template v-slot:prepend>
            <v-btn icon="mdi-phone" elevation="0"></v-btn>
          </template>
          <template v-slot:append>
            <v-btn
              variant="text"
              icon="mdi-chevron-left"
              @click.stop="railRight = !railRight"
            ></v-btn>
          </template>
        </v-list-item>

        <v-divider></v-divider>

        <v-list density="compact" nav>
          <v-list-item prepend-icon="mdi-home-city" title="Home" value="home"></v-list-item>
          <v-list-item prepend-icon="mdi-account" title="My Account" value="account"></v-list-item>
          <v-list-item prepend-icon="mdi-account-group-outline" title="Users" value="users"></v-list-item>
        </v-list>
      </v-navigation-drawer>

      <v-app-bar height="56" color="grey-lighten-2" elevation="2" :order="order">
        <template v-slot:prepend>
          <v-btn icon="mdi-heart"></v-btn> <h3>Jan, Vue 3 and Vuetify 3...</h3>
        </template>

        <template v-slot:append>
          <v-tooltip :text="`Darkmode: ${ theme === 'dark' ? 'aan' : 'uit' }`" location="bottom">
            <template v-slot:activator="{ props }">
              <v-btn rounded v-bind="props" :icon="theme === 'light' ? 'mdi-weather-sunny' : 'mdi-weather-night'" @click="onClick" />
            </template>
          </v-tooltip>
          <v-tooltip text="DevTools" location="bottom">
            <template v-slot:activator="{ props }">
              <v-btn rounded v-bind="props"
                     :icon="extraBar ? 'mdi-lock-open' : 'mdi-lock'"
                     @click="extraBar = !extraBar"
              />
            </template>
          </v-tooltip>
          <Settings />
          <v-btn icon="mdi-dots-vertical"></v-btn>
        </template>
      </v-app-bar>

      <v-app-bar location="bottom" height="48" color="grey-lighten-2" elevation="0">
        <p class="pa-4"> &copy; DotjeDotCom Productions 🌈</p>
      </v-app-bar>

      <v-main>
        <Search class="ma-2 pa-4"/>
        <v-card class="ma-2 pa-4">
          <HelloWorld  />
        </v-card>
      </v-main>
    </v-layout>
  </v-app>
</template>

<script lang="ts" setup>
import {ref} from 'vue'
import Clock from "@/components/Clock.vue";
import HelloWorld from "@/components/HelloWorld.vue";
import Settings from "@/components/Settings.vue";
import DevTools from "@/components/DevTools.vue";
import Search from "@/components/Search.vue";

const changeOrder = () => (order.value = order.value ??= '-1')
const onClick = () => (theme.value = theme.value === 'light' ? 'dark' : 'light')

const drawer = ref(true)
const extraBar = ref(false)
const order = ref('0')
const rail = ref(true)
const railRight = ref(true)
const theme = ref('dark')
</script>
