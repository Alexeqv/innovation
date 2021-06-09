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
        :page.sync="page"
        :items-per-page="itemsPerPage"
        @page-count="pageCount = $event"
      >
        <template v-slot:body="{ items }">
          <tbody>
            <tr v-for="item in items" :key="item.name" @click="go(item)">
              <td>{{ item.name }}</td>
              <td class="text-right">
                <v-btn icon>
                  <v-icon color="grey lighten-1">mdi-information</v-icon>
                </v-btn>
              </td>
            </tr>
          </tbody>
        </template>
      </v-data-table>
      <div class="text-center pt-2">
        <v-pagination circle v-model="page" :length="pageCount" @next="next"></v-pagination>
      </div>
    </v-card>
  </div>
</template>

<script>
export default {
  props: ["data", "from"],
  data: (vm) => ({
    search: "",
    page: 1,
    pageCount: 0,
    itemsPerPage: 7,
  }),
  methods: {
    next() {
      this.$emit('next');
    },
    go(item) {
      let id = item.url.substring(item.url.length - 3, item.url.length);
      id = id.replace(/\//gi, "");
      this.$router.push("/"+this.from+"/" + id);
    },
  },
};
</script>
