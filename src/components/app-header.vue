<template>
  <v-app-bar
    app
    :color="theme.isDark ? '#272727' : '#fff'"
    flat
    outlined
    extension-height="20"
  >
    <v-app-bar-nav-icon v-if="drawer === false" @click="drawer = !drawer">
    </v-app-bar-nav-icon>
    <v-spacer></v-spacer>
    <v-badge bordered top color="red accent-4" dot offset-x="10" offset-y="10">
      <v-icon> mdi-bell </v-icon>
    </v-badge>
    <div class="mx-3"></div>
    <v-avatar color="indigo" size="40">
      <v-icon dark> mdi-account-circle </v-icon>
    </v-avatar>
    <template slot="extension">
      <v-divider></v-divider>
    </template>
  </v-app-bar>
</template>

<script>
export default {
  name: "app-header",
  inject: {
    theme: {
      default: { isDark: false },
    },
  },
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
