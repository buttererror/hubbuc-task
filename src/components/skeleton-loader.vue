<template>
  <v-row>
    <v-col v-for="c in cols" :key="c" :cols="12 / cols">
      <v-skeleton-loader
        v-for="n in rows"
        :key="n"
        class="my-3 mx-auto"
        max-width="374"
        type="image"
      ></v-skeleton-loader>
    </v-col>
  </v-row>
</template>
<script>
export default {
  name: "skeleton-loader",
  props: {
    cols: {
      type: Number,
      required: true,
    },
    rows: {
      type: Number,
      required: true,
    },
  },
};
</script>
