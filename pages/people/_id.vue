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
        <v-row align="center" class="mx-0" v-if="false">
          <v-rating
            :value="4.5"
            color="amber"
            dense
            half-increments
            readonly
            size="14"
          ></v-rating>

          <div class="grey--text ms-4">4.5 (413)</div>
        </v-row>

        <v-simple-table>
          <template v-slot:default>
            <tbody>
              <tr>
                <td>Height</td>
                <td v-text="data.height" />
              </tr>
              <tr>
                <td>Eye Color</td>
                <td v-text="data.eye_color" />
              </tr>
              <tr>
                <td>Gender</td>
                <td v-text="data.gender" />
              </tr>
              <tr>
                <td>Starships</td>
                <td v-text="data.starships.length" />
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
    img: require("~/assets/img/people.png"),
    ready: false,
    data: null,
    selection: 1,
  }),
  head() {
    return {
      title: "People",
      meta: [
        {
          hid: "people",
          name: "people",
          content: "people",
        },
        {
          name: "keywords",
          content: "people",
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
      axios["get"](process.env.api_url + "people/" + vm.$route.params.id, {
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
