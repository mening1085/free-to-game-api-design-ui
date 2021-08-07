<template>
  <v-app>
    <!-- Navbar -->
    <Navbar />

    <!-- Content -->
    <v-main class="bg">
      <div class="container">
        <v-row>
          <!-- left -->
          <v-col cols="8">
            <div>
              <h2>Recently Added</h2>
            </div>

            <v-card
              color="#32383D"
              elevation="2"
              v-for="(item, i) in games.slice(0, 3)"
              :key="i"
              class="pa-4 mb-4"
            >
              <v-layout class="d-flex justify-end align-center">
                <v-flex xs3 class="mx-3">
                  <v-img
                    style="border-radius: 4px"
                    :src="item.thumbnail"
                  ></v-img>
                </v-flex>
                <v-flex xs7 class="mx-3 align-center">
                  <div style="color: #aaa">
                    <h3>{{ item.title }}</h3>
                  </div>
                  <div style="color: #798287" class="desc mb-1">
                    {{ item.short_description }}
                  </div>
                  <div>
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
                  </div>
                </v-flex>
                <v-flex xs2>
                  <v-btn small depressed color="#4799EB" dark>
                    FREE
                  </v-btn>
                </v-flex>
              </v-layout>
            </v-card>
          </v-col>

          <!-- right -->
          <v-col cols="4">
            <div>
              <h2>Most Played Today</h2>
            </div>
            <v-card
              class="mb-3"
              elevation="2"
              v-for="(item, i) in games.slice(0, 2)"
              :key="i"
            >
              <v-img :src="item.thumbnail"></v-img>
            </v-card>
          </v-col>
        </v-row>

        <v-row>
          <v-col
            class="pa-2"
            v-for="(item, i) in games.slice(3, 100)"
            :key="i"
            cols="3"
          >
            <v-img :src="item.thumbnail"></v-img>
          </v-col>
        </v-row>
      </div>
    </v-main>
  </v-app>
</template>

<script>
import Navbar from "./components/Navbar.vue";
import axios from "axios";

export default {
  name: "App",
  components: {
    Navbar,
  },

  data() {
    return {
      games: null,
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

    this.games = res.slice(0, 99);
    // this.games = res.slice(0, 10);
  },

  methods: {
    // Function
  },
};
</script>

<style lang="css">
.bg {
  background: #272b30;
  color: #aaa;
}
.desc {
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}
</style>
