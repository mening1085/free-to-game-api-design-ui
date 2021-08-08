<template>
  <div class="container">
    <v-layout wrap class="d-flex align-center">
      <!-- left -->
      <v-flex xs12 sm6>
        <v-img :src="data.thumbnail"></v-img>
      </v-flex>

      <!-- right -->
      <v-flex xs12 sm6 class="px-5">
        <div>
          <h1>
            {{ data.title }}
          </h1>
        </div>
        <p>{{ data.short_description }}</p>
        <div>หมวดหมู่ : {{ data.genre }}</div>
        <div>Platform : {{ data.platform }}</div>
        <br />
        <div>Publisher : {{ data.publisher }}</div>
        <div>Developer : {{ data.developer }}</div>
        <br />
        <div>ปีที่ผลิต : {{ data.release_date }}</div>
      </v-flex>
    </v-layout>

    <br />
    <h2>รายละเอียดเกม</h2>
    <p>
      {{ data.description }}
    </p>

    <v-layout wrap>
      <v-flex xs6 v-for="(item, i) in data.screenshots" :key="i">
        <v-img :src="item.image"></v-img>
      </v-flex>
    </v-layout>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      data: null,
    };
  },

  async created() {
    var options = {
      method: "GET",
      url: "https://free-to-play-games-database.p.rapidapi.com/api/game",
      params: { id: this.$route.params.id },
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

    console.log(res);
    this.data = res;
  },
};
</script>

<style></style>
