<template>
  <v-card>
    <v-toolbar color="#363062" dark flat>
      <v-toolbar-title class="font-weight-bold">Sales Record</v-toolbar-title>
      <v-spacer></v-spacer>

      <template v-slot:extension>
        <v-tabs v-model="tab" align-with-title>
          <v-tabs-slider color="#D8B9C3"></v-tabs-slider>

          <v-tab v-for="item in items" :key="item">
            {{ item }}
          </v-tab>
        </v-tabs>
      </template>
    </v-toolbar>

    <v-tabs-items v-model="tab">
      <!-- ORDER IN PROCESS -->
      <v-tab-item>
        <v-card flat>
          <v-card-text> <order-process></order-process> </v-card-text>
        </v-card>
      </v-tab-item>

      <!-- FINISHED ORDER -->
      <v-tab-item>
        <v-card flat>
          <v-card-text> <order-finished></order-finished> </v-card-text>
        </v-card>
      </v-tab-item>
    </v-tabs-items>
  </v-card>
</template>

<script>
export default {
  head() {
    return {
      title: "Sales",
    };
  },
  data() {
    return {
      tab: null,
      items: ["Order in process", "Finished Order"],
    };
  },
};
</script>