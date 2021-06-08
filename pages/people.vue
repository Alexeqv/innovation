<template>
  <div>
    <h2 class="mt-5 mb-6">People</h2>
    <v-card>
      <Datatable :data="dataList" />
    </v-card>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: (vm) => ({
    dataList: {
      headers: [
        {
          text: "Name",
          align: "start",
          value: "name",
        },
      ],
      desserts: [],
      options: {
        sortBy: [],
      },
    },
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
      axios["get"](process.env.api_url + "people", {
        headers: {
          "Content-Type": "application/json",
        },
      })
        .then((response) => {
          console.log("response", response);
          vm.dataList.desserts = response.data.results;
          //   this.$nuxt.$emit("showLoading", false);
        })
        .catch((error) => {
          console.log("getPeople", error);
        });
    },
  },
  mounted() {
    setTimeout(() => {
      this.$nuxt.$emit("headerTitle", "Prueba Ténica");
      this.$nuxt.$emit("urlBack", "/", "push");
    }, 500);

    this.getPeople();
  },
};
</script>
