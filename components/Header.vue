<template>
  <div>
    <v-app-bar light app color="white">
      <v-btn v-if="btnBack" icon @click="goBack">
        <v-icon> mdi-chevron-left </v-icon>
      </v-btn>

      <img
        v-if="isLogo"
        src="https://www.innovation.es/img/logo.png"
        alt="logo innovation"
        style="width: 90px"
      />
      <v-toolbar-title class="pl-5" v-if="isTitle">{{ title }} </v-toolbar-title>

      <v-spacer></v-spacer>
    </v-app-bar>
  </div>
</template>
<script>
export default {
  data: (vm) => ({
      urlLogo: "",
      isLogo: true,
      isTitle: true,
      btnBack: false,
      title: "",
      urlBack: ""
  }),
  created() {
    this.$nuxt.$on("headerTitle", (title) => {
      this.isTitle = true;
      this.title = title;
    });
    this.$nuxt.$on("headerLogo", (url) => {
      this.isLogo = true;
      this.urlLogo = url;
    });
    this.$nuxt.$on("urlBack", (url, type) => {
     /*  this.btnBack = true;
      this.type = type;
      this.urlBack = url; */
    });
    this.$nuxt.$on("showBtnBack", (option) => {
      // this.btnBack = option;
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
