<template>
  <div>
    <!-- content -->
    <div class="container">
      <v-row>
        <!-- left -->
        <v-col cols="12" sm="8" md="8">
          <div>
            <h2>Recently Added</h2>
          </div>

          <v-card
            color="#32383D"
            elevation="2"
            v-for="(item, i) in gamesRecentlyAdded"
            :key="i"
            class="pa-4 mb-4"
            @click="getDetail(item.id)"
          >
            <v-layout wrap class="d-flex justify-end align-center">
              <v-flex xs4 md3 class="px-1 px-md-3">
                <v-img style="border-radius: 4px" :src="item.thumbnail"></v-img>
              </v-flex>

              <v-flex xs8 md7 class="px-1 px-md-3 align-center">
                <div style="color: #aaa">
                  <h3>{{ item.title }}</h3>
                </div>
                <div style="color: #798287" class="desc mb-1">
                  {{ item.short_description }}
                </div>
                <div>
                  <v-layout>
                    <v-flex shrink>
                      <v-btn
                        height="20"
                        class="px-1"
                        depressed
                        small
                        color="#aaa"
                        dark
                      >
                        <span style="color: #32383D">
                          {{ item.genre }}
                        </span>
                      </v-btn>
                    </v-flex>

                    <v-spacer></v-spacer>

                    <v-flex shrink v-if="$vuetify.breakpoint.smAndDown">
                      <v-btn
                        height="20"
                        class="px-1"
                        small
                        depressed
                        color="#4799EB"
                        dark
                      >
                        FREE
                      </v-btn>
                    </v-flex>
                  </v-layout>
                </div>
              </v-flex>

              <v-flex xs2 sm2 md2 v-if="$vuetify.breakpoint.mdAndUp">
                <v-btn small depressed color="#4799EB" dark>
                  FREE
                </v-btn>
              </v-flex>
            </v-layout>
          </v-card>
        </v-col>

        <!-- right -->
        <v-col cols="12" sm="4" md="4">
          <div>
            <h2>Most Played Today</h2>
          </div>
          <v-card
            class="mb-3"
            elevation="2"
            v-for="(item, i) in gamesMostPlayedToday"
            :key="i"
            @click="getDetail(item.id)"
          >
            <v-img :src="item.thumbnail"></v-img>
          </v-card>
        </v-col>
      </v-row>

      <div class="mb-2">
        <h2>All Games</h2>
      </div>
      <v-row>
        <v-col
          class="pa-2"
          v-for="(item, i) in allGames"
          :key="i"
          cols="6"
          sm="4"
          md="3"
          @click="getDetail(item.id)"
        >
          <v-card elevation="2" style="cursor: pointer">
            <v-img :src="item.thumbnail"></v-img>
          </v-card>
        </v-col>
      </v-row>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "Home",
  data() {
    return {
      gamesRecentlyAdded: null,
      gamesMostPlayedToday: null,
      allGames: null,
    };
  },

  async created() {
    var options = {
      method: "GET",
      url: "https://free-to-play-games-database.p.rapidapi.com/api/games",
      headers: {
        "x-rapidapi-key": "bf3353835emsh6fc47102e25e082p1bc844jsneccc6e65d0f1",
        "x-rapidapi-host": "free-to-play-games-database.p.rapidapi.com",
      },
    };
    const res = await axios
      .request(options)
      .then(function(response) {
        return response.data;
      })
      .catch(function(error) {
        console.error(error);
      });

    this.gamesRecentlyAdded = res.slice(0, 3);
    this.gamesMostPlayedToday = res.slice(0, 2);
    this.allGames = res.slice(3, 99);
  },

  methods: {
    // Function
    getDetail(id) {
      console.log(id);
      this.$router.push(`/detail/${id}`);
    },
  },
};
</script>
