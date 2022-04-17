<template>
  <v-row justify="center" align="center">
    <v-col cols="12" sm="12" md="12">
      <v-card>
        <v-data-table :items="routers" :headers="headers"> </v-data-table>
      </v-card>
    </v-col>
  </v-row>
</template>

<script lang="ts">
import Vue from "vue";

interface Router {
  alias: string;
  path: string;
  controller: string;
  action: string;
}

interface VueData {
  name: string;
  routers: Router[];
  headers: { text: string; value: keyof Router }[];
}

export default Vue.extend({
  mounted() {
    this.getAPI();
  },
  methods: {
    async getAPI() {
      const url = `/api/v1/controllers`;
      const { data } = await this.$axios.get(url);
      this.routers = data;
    },
  },
  data(): VueData {
    return {
      name: "IndexPage",
      routers: [],
      headers: [
        { text: "エイリアス", value: "alias" },
        { text: "パス", value: "path" },
        { text: "コントローラー", value: "controller" },
        { text: "アクション", value: "action" },
      ],
    };
  },
});
</script>
