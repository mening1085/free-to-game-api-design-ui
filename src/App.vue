<template>
  <v-app>
    <!-- Navbar -->
    <Navbar />

    <!-- Content -->
    <v-main class="bg">
      <router-view></router-view>
    </v-main>
  </v-app>
</template>

<script>
import Navbar from "./components/Navbar.vue";
export default {
  name: "App",
  components: {
    Navbar,
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
