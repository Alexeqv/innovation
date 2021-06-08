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
  </v-main>

  <!-- Footer -->
  <Footer />
</v-app>
</template>

<script>
export default {
  data () {
    return {
     
    }
  }
}
</script>