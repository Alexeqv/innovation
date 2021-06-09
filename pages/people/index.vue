<template>
  <div>
    <h2 class="mt-5 mb-6">People</h2>
    <v-card style="margin-bottom: 45px;">
      <Skeletonloader v-if="!ready" />
      <Datatable v-else @next="nextin"  from="people" :data="dataList" />
    </v-card>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: (vm) => ({
    ready: false,
    nextUrl: null,
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
    nextin() {
      const vm = this;
      this.getPeople(true);
    },
    getPeople(next = false) {
      const vm = this;
      let url = next ? vm.nextUrl : process.env.api_url + "people"
      axios["get"](url, {
        headers: {
          "Content-Type": "application/json",
        },
      })
        .then((response) => {
          // console.log("response", response);
          if (next) {
            var arrayOld = vm.dataList.desserts;
            var arrayNew = response.data.results;
            vm.dataList.desserts = arrayOld.concat(arrayNew);
          }
          else {
            vm.dataList.desserts = response.data.results;
          }
          vm.nextUrl = response.data.next;
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
      this.$nuxt.$emit("urlBack", "/", "push");
    }, 500);

    this.getPeople();
  },
};
</script>
