<template>
  <div>
    <h2 class="mt-5">Star Wars</h2>
    <v-card class="mx-auto mt-5" max-width="400">
      <v-list>
        <v-list-item-group v-model="model" mandatory color="indigo">
          <v-list-item v-for="(item, i) in items" :key="i" :to="item.to">
            <v-list-item-avatar>
              <!-- <v-img :src="item.icon"></v-img> -->
              <v-img
                :src="item.icon"
                :lazy-src="item.icon"
                aspect-ratio="1"
                class="grey lighten-2"
              >
                <template v-slot:placeholder>
                  <v-row
                    class="fill-height ma-0"
                    align="center"
                    justify="center"
                  >
                    <v-progress-circular
                      indeterminate
                      color="grey lighten-5"
                    ></v-progress-circular>
                  </v-row>
                </template>
              </v-img>
            </v-list-item-avatar>

            <v-list-item-content>
              <v-list-item-title v-text="item.text"></v-list-item-title>
            </v-list-item-content>
          </v-list-item>
        </v-list-item-group>
      </v-list>
    </v-card>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: (vm) => ({
    items: [
      {
        icon: require('~/assets/img/people.png'),
        text: "People",
        to: "/people",
      },
      {
        icon: require('~/assets/img/starships.webp'),
        text: "Starships",
        to: "/starships",
      },
      {
        icon: require('~/assets/img/planets.jpg'),
        text: "Planets",
        to: "/planets",
      },
    ],
    model: 1,
  }),
  head() {
    return {
      title: "Home",
      meta: [
        {
          hid: "home",
          name: "home",
          content: "home",
        },
        {
          name: "keywords",
          content: "home",
        },
      ],
    };
  },
  layout(context) {
    return "default";
  },
  mounted() {
    setTimeout(() => {
      this.$nuxt.$emit("headerTitle", "Prueba Ténica");
      this.$nuxt.$emit("showBtnBack", false);
    }, 500);
    setTimeout(() => {
      this.$nuxt.$emit("showLoading", false);
    }, 3000);
  },
};
</script>
