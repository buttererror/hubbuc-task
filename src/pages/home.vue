<template>
  <div>
    <skeleton-loader v-if="loading" :cols="4" :rows="5" />
    <v-row v-else>
      <v-col v-for="column in columns" :key="column.id" :cols="column.cols">
        <v-list>
          <v-subheader>{{ column.title }}</v-subheader>
          <draggable
            v-for="item in column.list"
            :key="item.id"
            :list="column.list"
            group="people"
          >
            <!--          <v-list-item-group color="primary">-->
            <v-list-item>
              <v-card class="mx-auto my-3 w-100" max-width="374">
                <v-card-title>{{ item.name }}</v-card-title>

                <!--            <v-card-text>-->
                <!--              <v-row align="center" class="mx-0">-->
                <!--                <v-rating-->
                <!--                  :value="4.5"-->
                <!--                  color="amber"-->
                <!--                  dense-->
                <!--                  half-increments-->
                <!--                  readonly-->
                <!--                  size="14"-->
                <!--                ></v-rating>-->

                <!--                <div class="grey--text ms-4">4.5 (413)</div>-->
                <!--              </v-row>-->

                <!--              <div class="my-4 text-subtitle-1">$ • Italian, Cafe</div>-->

                <!--              <div>-->
                <!--                Small plates, salads & sandwiches - an intimate setting with 12-->
                <!--                indoor seats plus patio seating.-->
                <!--              </div>-->
                <!--            </v-card-text>-->

                <!--            <v-divider class="mx-4"></v-divider>-->

                <!--            <v-card-title>Tonight's availability</v-card-title>-->

                <!--            <v-card-text>-->
                <!--              <v-chip-group-->
                <!--                active-class="deep-purple accent-4 white--text"-->
                <!--                column-->
                <!--              >-->
                <!--                <v-chip>5:30PM</v-chip>-->

                <!--                <v-chip>7:30PM</v-chip>-->

                <!--                <v-chip>8:00PM</v-chip>-->

                <!--                <v-chip>9:00PM</v-chip>-->
                <!--              </v-chip-group>-->
                <!--            </v-card-text>-->
              </v-card>
            </v-list-item>
            <!--          </v-list-item-group>-->
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
