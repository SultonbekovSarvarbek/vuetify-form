<template>
  <v-app class="custom-vuetify">
    <v-main class="grey lighten-3">
      <v-container>
        <router-view></router-view>
      </v-container>
    </v-main>
  </v-app>
</template>
<script>
export default {
  name: "App",
  data: () => ({})
};
</script>

<style lang="scss">
@import "@/assets/font/font.scss";
html,
body {
  font-weight: 300;
  font-family: "Roboto", sans-serif;
}
</style>
