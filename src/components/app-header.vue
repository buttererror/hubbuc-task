<template>
  <v-app-bar app color="#fff" flat outlined extension-height="20">
    <v-app-bar-nav-icon v-if="drawer === false"
      @click="drawer = !drawer">
    </v-app-bar-nav-icon>
    <template slot="extension">
      <v-divider></v-divider>
    </template>
  </v-app-bar>
</template>

<script>
export default {
  name: "app-header",
  computed: {
    drawer: {
      get() {
        return this.$store.state.drawer;
      },
      set(value) {
        this.$store.commit("updateDrawer", value);
      },
    },
  },
};
</script>

<style scoped></style>
