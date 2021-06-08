<template>
  <div>
    <h2 class="mt-5">Star Wars</h2>
    <v-card class="mx-auto mt-5" max-width="400">
      <v-list>
        <v-list-item-group v-model="model" mandatory color="indigo">
          <v-list-item v-for="(item, i) in items" :key="i" :to="item.to">
            <v-list-item-avatar>
              <v-img :src="item.icon"></v-img>
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
        icon: "https://cdn0.iconfinder.com/data/icons/people-avatars-9/24/people_avatar_head_star_wars_storm_trooper-512.png",
        text: "People",
        to: '/people'
      },
      {
        icon: "https://cdn4.iconfinder.com/data/icons/star-wars-9/100/millennium_falcon-512.png",
        text: "Starships",
        to: '/starships'
      },
      {
        icon: "https://library.kissclipart.com/20180907/hce/kissclipart-death-star-drawing-png-clipart-death-star-anakin-s-24fd48aba5544bc7.jpg",
        text: "Planets",
        to: '/planets'
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
  },
};
</script>
