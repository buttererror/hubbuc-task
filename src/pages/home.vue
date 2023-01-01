<template>
  <div>
    <skeleton-loader v-if="loading" :cols="4" :rows="5" />
    <v-row v-else>
      <v-col v-for="column in columns" :key="column.id" :cols="column.cols">
        <v-list>
          <v-subheader>{{ column.title }}</v-subheader>
          <draggable
            :list="column.list"
            group="beers"
            style="min-height: 500px"
          >
            <v-list-item
              v-for="item in column.list"
              :key="item.id"
              class="my-2"
            >
              <v-card class="mx-auto my-3 w-100" max-width="374">
                <v-card-title>{{ item.name }}</v-card-title>
                <v-card-text>
                  <div class="my-4 text-subtitle-1">
                    {{ item.brand }}
                  </div>
                  <div>
                    {{ item.yeast }}
                  </div>
                </v-card-text>

                <v-divider class="mx-4"></v-divider>

                <v-card-text>
                  <v-chip-group
                    active-class="deep-purple accent-4 white--text"
                    column
                  >
                    <v-chip v-if="item.alchol"
                      >alcohol: {{ item.alchol }}</v-chip
                    >

                    <!--                    <v-chip>brand: {{ item.brand }}</v-chip>-->

                    <v-chip v-if="item.hop">hop: {{ item.hop }}</v-chip>

                    <v-chip v-if="item.style">style: {{ item.style }}</v-chip>
                  </v-chip-group>
                </v-card-text>
              </v-card>
            </v-list-item>
          </draggable>
        </v-list>
      </v-col>
    </v-row>
  </div>
</template>
<script>
import draggable from "vuedraggable";
import SkeletonLoader from "@/components/skeleton-loader";

export default {
  name: "Home",
  components: {
    SkeletonLoader,
    draggable,
  },
  data() {
    return {
      loading: true,
      columns: [
        {
          id: 0,
          title: "List 1",
          cols: 3,
          list: [],
        },
        {
          id: 1,
          title: "List 2",
          cols: 3,
          list: [],
        },
        {
          id: 2,
          title: "List 3",
          cols: 3,
          list: [],
        },
        {
          id: 3,
          title: "List 4",
          cols: 3,
          list: [],
        },
      ],
    };
  },
  created() {
    let req = new XMLHttpRequest();
    req.open(
      "GET",
      "https://random-data-api.com/api/v2/beers?size=20&response_type=json"
    );
    req.send();
    req.onreadystatechange = () => {
      if (req.readyState == 4 && req.status == 200) {
        let responseData = JSON.parse(req.responseText);
        let sliceStarts = 0;
        let sliceEnds = 5;
        this.columns.forEach((x) => {
          x.list = responseData.slice(sliceStarts, sliceEnds);
          sliceStarts += 5;
          sliceEnds += 5;
        });
        this.loading = false;
      }
    };
  },
};
</script>
