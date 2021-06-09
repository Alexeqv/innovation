<template>
  <div>
    <Skeletonloader v-if="!ready" />
    <v-card v-else class="mx-auto my-12" max-width="374">
      <template slot="progress">
        <v-progress-linear
          color="deep-purple"
          height="10"
          indeterminate
        ></v-progress-linear>
      </template>

      <v-img height="250" :src="img"></v-img>

      <v-card-title v-text="data.name" />

      <v-card-text>
        <v-row align="center" class="mx-0 mb-5">
          <v-rating
            :value="data.hyperdrive_rating"
            color="amber"
            dense
            half-increments
            readonly
            size="14"
          ></v-rating>

          <div class="grey--text ms-4">{{data.hyperdrive_rating}} (Hyper Driver)</div>
        </v-row>

        <v-simple-table>
          <template v-slot:default>
            <tbody>
              <tr>
                <td>Cargo Capacity</td>
                <td v-text="data.cargo_capacity" />
              </tr>
              <tr>
                <td>Consumables</td>
                <td v-text="data.consumables" />
              </tr>
              <tr>
                <td>Passengers</td>
                <td v-text="data.passengers" />
              </tr>
              <tr>
                <td>Pilots</td>
                <td v-text="data.pilots.length" />
              </tr>
              <tr>
                <td>films</td>
                <td v-text="data.films.length" />
              </tr>
            </tbody>
          </template>
        </v-simple-table>
      </v-card-text>
    </v-card>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: (vm) => ({
    img: require("~/assets/img/starships.webp"),
    ready: false,
    data: null,
    selection: 1,
  }),
  head() {
    return {
      title: "Starships",
      meta: [
        {
          hid: "starships",
          name: "starships",
          content: "starships",
        },
        {
          name: "keywords",
          content: "starships",
        },
      ],
    };
  },
  layout(context) {
    return "default";
  },
  methods: {
    getPeople() {
      const vm = this;
      axios["get"](process.env.api_url + "starships/" + vm.$route.params.id, {
        headers: {
          "Content-Type": "application/json",
        },
      })
        .then((response) => {
        //   console.log("response", response.data);
          vm.data = response.data;
          vm.ready = true;
          vm.$nuxt.$emit("showLoading", false);
        })
        .catch((error) => {
          console.log("getPeople", error);
        });
    },
  },
  mounted() {
    setTimeout(() => {
      this.$nuxt.$emit("headerTitle", "Prueba Ténica");
      this.$nuxt.$emit("urlBack", "-1", "go");
    }, 500);

    this.getPeople();
  },
};
</script>
