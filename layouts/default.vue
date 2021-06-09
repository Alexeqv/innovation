<template>
  <v-app>
    <!-- Sizes your content based upon application components -->
    <v-main>
      <!-- Header -->
      <Header />

      <!-- Provides the application the proper gutter -->
      <v-container fluid>
        <!-- If using vue-router -->
        <nuxt />
      </v-container>
      <v-overlay :value="overlay">
        <v-dialog v-model="overlay" hide-overlay persistent fullscreen>
          <v-card color="white" light>
            <v-card-text class="py-10 text-center">
              <div id="loading">
                <span></span>
              </div>
               <!-- <h3 class="font-wight-regular" style="position: relative; top: -20px;">Procesando</h3> -->
              <!-- <v-progress-linear
                indeterminate
                color="warning"
                class="mb-3"
              ></v-progress-linear> -->
            </v-card-text>
          </v-card>
        </v-dialog>
      </v-overlay>
    </v-main>

    <!-- Footer -->
    <Footer />
  </v-app>
</template>

<script>
export default {
  data() {
    return {
      overlay: true,
    };
  },
  created() {
    this.$nuxt.$on("showLoading", (option) => {
      this.overlay = option;
    });
  },
};
</script>

<style scoped>
#loading {
  position: fixed;
  z-index: 999999;
  top: 0;
  left: 0;
  width: 100%;
  height: 100vh;
  background-color: white;
  display: flex;
  flex-wrap: wrap;
  align-items: center;
  align-content: center;
  justify-content: center;
}
#loading span {
  display: block;
  position: relative;
  top: 15px;
  width: 8px;
  height: 40px;
  background-color: #ffc823;
  animation: loading_move 2s infinite;
}

@keyframes loading_move {
  0% {
    transform: translate(-200%);
    background-color: #ffc823;
  }
  25% {
    transform: translate(200%);
    background-color: #c9dd0a;
  }
  50% {
    transform: translate(-200%);
    background-color: #00b1c1;
  }
  75% {
    transform: translate(200%);
    background-color: #7c7b7f;
  }
  100% {
    transform: translate(-200%);
    background-color: #ffc823;
  }
}
</style>