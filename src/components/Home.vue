<template>
  <v-main>
    <v-container>
      <v-row justify="center">
        <v-col cols="12" sm="8" md="6" class="d-flex align-center">
          <v-text-field
            label="Type your search here"
            v-model="textInput"
            class="pink-input"
          >
          </v-text-field>

          <v-btn
            color="pink"
            variant="flat"
            rounded="xl"
            @click="searchDeals()"
          >
            Search <v-icon end icon="mdi-magnify"></v-icon>
          </v-btn>
        </v-col>
      </v-row>

      <v-row justify="center">
        <v-progress-circular
          color="pink"
          v-if="loading"
          indeterminate
        ></v-progress-circular>
      </v-row>

      <v-row justify="center" v-if="!loading">
        <v-col cols="12">
          <v-row>
            <v-col
              v-for="deal in dealList"
              :key="deal.id"
              cols="12"
              sm="6"
              md="3"
              lg="3"
            >
              <v-card class="mx-auto my-12" max-width="374">
                <v-img cover :src="deal.thumb"></v-img>
                <span> </span>
                <v-chip color="pink" variant="flat" class="savings">
                  {{ deal.savings.substr(0, 2) }} % off
                </v-chip>

                <v-card-item>
                  <v-card-title>{{ deal.title }}</v-card-title>

                  <v-card-subtitle class="text-center">
                    <span class="me-1">Steam Review</span>
                  </v-card-subtitle>
                </v-card-item>

                <v-card-text>
                  <v-row align="center" class="mx-0 justify-center">
                    <div class="rating">
                      <v-icon
                        v-for="index in 5"
                        :key="index"
                        :color="getStarColor(index, deal.steamRatingPercent)"
                        >mdi-star</v-icon
                      >
                    </div>
                  </v-row>
                </v-card-text>

                <v-card-actions class="my-3 justify-center">
                  <v-btn
                    elevation="6"
                    color="pink"
                    class="white--text"
                    variant="flat"
                    size="x-large"
                  >
                    <span class="normalPrice"> $ {{ deal.normalPrice }} </span>
                    $ {{ deal.salePrice }}
                  </v-btn>
                </v-card-actions>
              </v-card>
            </v-col>
          </v-row>
        </v-col>
      </v-row>
    </v-container>
  </v-main>
</template>

<style>
.pink-input {
  color: #f72d70 !important;
}
.normalPrice {
  font-size: 10px;
  text-decoration: line-through;
  margin-right: 5px;
}
.savings {
  position: absolute !important;
  top: 30px !important;
  right: 30px !important;
}
.rating {
  color: gold;
}
</style>





<script>
import axios from "axios";

export default {
  async created() {
    try {
      this.loading = true;
      let deals = await axios.get("http://127.0.0.1:8000/api/v1/deals");
      this.dealList = deals.data;
      this.loading = false;
    } catch (error) {
      console.log(error);
    }
  },
  data() {
    return {
      textInput: "",
      dealList: [],
      loading: false,
    };
  },
  methods: {
    async searchDeals() {
      try {
        const url = `http://127.0.0.1:8000/api/v1/deals?q=${this.textInput}`;
        this.loading = true;
        let deals = await axios.get(url);
        this.dealList = deals.data;
        this.loading = false;
      } catch (error) {
        console.log(error);
      }
    },
    getStarColor(index, steamRatingPercent) {
      const filledStars = Math.floor(steamRatingPercent / 20);
      if (index <= filledStars) {
        return "gold"; // Estrella llena
      } else {
        return "grey"; // Estrella vacía
      }
    },
  },
};
</script>