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

      <v-navigation-drawer width="500" color="grey-darken-1" v-if="extraBar" permanent>
        <h4 class="pa-4">DevTools BOOM 💥</h4>
      </v-navigation-drawer>

      <v-app-bar height="56" color="grey" elevation="0">
        <template v-slot:prepend>
          <v-btn icon="mdi-clock"></v-btn> {{ time }}
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

      <v-app-bar color="grey-lighten-2" elevation="2" :order="order">

        <template v-slot:prepend>
          <v-btn icon="mdi-heart"></v-btn> <h3>Jan, Vue 3 and Vuetify 3...</h3>
        </template>

        <template v-slot:append>

          <v-btn rounded :icon="theme === 'light' ? 'mdi-weather-sunny' : 'mdi-weather-night'" @click="onClick" />

          <v-btn rounded
                 :icon="extraBar ? 'mdi-lock-open' : 'mdi-lock'"
                 @click="extraBar = !extraBar"
          />

          <v-btn icon="mdi-dots-vertical"></v-btn>

        </template>
      </v-app-bar>

      <v-app-bar location="bottom" height="48" color="grey-lighten-2" elevation="0">
        <p class="pa-4"> &copy; DotjeDotCom Productions 🌈</p>
      </v-app-bar>

      <v-main>
        <v-card height="200px" class="d-flex justify-center align-center pa-4">
          <h1 class="pa-4">Zoeken:</h1>
          <v-text-field
            density="compact"
            variant="solo"
            label="Hup hup zoeken, klanten worden niet zelf gebeld.."
            append-inner-icon="mdi-magnify"
            single-line
            hide-details

          ></v-text-field>
<!--          @click:append-inner="onClick"-->
        </v-card>
        <HelloWorld />
      </v-main>


    </v-layout>

  </v-app>

</template>

<script lang="ts" setup>
import {ref, reactive, computed} from 'vue'
import HelloWorld from "@/components/HelloWorld.vue";
import { useIntervalFn} from "@vueuse/core";
import dayjs from "dayjs";

const theme = ref('light')
const order = ref('-1')
function onClick () {
  theme.value = theme.value === 'light' ? 'dark' : 'light'
}
const drawer = ref(true)
const items = reactive([
  { title: 'Home', icon: 'mdi-home-city' },
  { title: 'My Account', icon: 'mdi-account' },
  { title: 'Users', icon: 'mdi-account-group-outline' },
])
const rail = ref(true)
const railRight = ref(true)
const date = computed(()=> new Date().toISOString())
const changeOrder = () => {
  order.value = order.value ??= '-1'
}

const extraBar = ref(false)
const time = ref('')
const interval = ref(1000)
const { pause, resume, isActive } = useIntervalFn(() => {
  console.log(dayjs().format('hh:mm:ss'))
  time.value = dayjs().format('hh:mm:ss')
}, interval)
</script>
