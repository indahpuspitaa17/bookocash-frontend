<template>
  <v-theme-provider>
    <v-app class="gradient-play">
      <div class="spacing-small"></div>
      <nuxt />
      <div class="spacing-small"></div>
    </v-app>
  </v-theme-provider>
</template>

<script>
export default {};
</script>

<style scoped>
.gradient-play {
  background: #363062;
  background-size: 100%;
}
</style>
