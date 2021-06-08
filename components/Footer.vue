<template>
  <v-footer light color="white" app>
    <!-- -->
    <v-fab-transition v-if="btnBack">
      <v-btn
        color="black"
        fab
        small
        dark
        bottom
        left
        class="v-btn--back"
        @click="goBack"
      >
        <v-icon>mdi-arrow-left</v-icon>
      </v-btn>
    </v-fab-transition>
  </v-footer>
</template>
<script>
export default {
  data: (vm) => ({
      btnBack: false,
      urlBack: ""
  }),
  created() {
    this.$nuxt.$on("urlBack", (url, type) => {
      this.btnBack = true;
      this.type = type;
      this.urlBack = url;
    });
    this.$nuxt.$on("showBtnBack", (option) => {
      this.btnBack = option;
    });
  },
  methods: {
    goBack() {
      let vm = this;
      if (vm.type == "go") {
        vm.$router.go(vm.urlBack);
      } else if (vm.type == "push") {
        vm.$router.push(vm.urlBack);
      }
      // window.location.href = vm.urlBack;
    },
  }
};
</script>

<style scoped>
.v-btn--back {
    bottom: 10px !important;
}
</style>
