<template>
  <v-navigation-drawer app v-model="drawer">
    <v-app-bar
      :color="theme.isDark ? '#272727' : '#fff'"
      flat
      outlined
      extension-height="20"
    >
      <div class="d-flex justify-space-between align-center w-100">
        <v-img
          alt="logo"
          class="shrink mr-2"
          contain
          src="@/assets/img/logo.svg"
          transition="scale-transition"
          width="35"
        />
        <v-app-bar-nav-icon class="float-right" @click="drawer = !drawer">
        </v-app-bar-nav-icon>
      </div>
      <template slot="extension">
        <v-divider></v-divider>
      </template>
    </v-app-bar>
    <template slot="append">
      <div class="d-flex justify-center pa-2 text-center">
        <v-switch
          v-model="isDarkTheme"
          label="Dark mode"
          color="white"
        ></v-switch>
      </div>
    </template>
  </v-navigation-drawer>
</template>

<script>
export default {
  name: "side-bar",
  data() {
    return {
      isDarkTheme: false,
    };
  },
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
  watch: {
    isDarkTheme(value) {
      this.$vuetify.theme.dark = value;
    },
  },
};
</script>

<style scoped></style>
