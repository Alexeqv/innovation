<template>
  <div>
    <v-card>
      <v-card-title class="pb-0 mb-0">
        <v-text-field
          dense
          v-model="search"
          append-icon="mdi-magnify"
          label="Search"
        ></v-text-field>
      </v-card-title>
      <v-data-table
        :options="data.options"
        :headers="data.headers"
        :items="data.desserts"
        :search="search"
        hide-default-header
        hide-default-footer
      >
      </v-data-table>
    </v-card>
  </div>
</template>

<script>
export default {
  props: ["data"],
  data: (vm) => ({
    search: ""
  }),
};
</script>
