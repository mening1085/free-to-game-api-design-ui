<template>
  <div>
    <v-app-bar app color="#272B30" dark>
      <div class="d-flex align-center">
        <v-icon style="font-size: 56px;" class="mr-2">
          mdi-gamepad-variant
        </v-icon>
        <div class="title">
          Free to Game
        </div>
      </div>

      <v-spacer></v-spacer>

      <div>
        <v-text-field
          outlined
          hide-details
          dense
          placeholder="search"
          prepend-inner-icon="mdi-magnify"
        ></v-text-field>
      </div>
    </v-app-bar>
  </div>
</template>

<script>
export default {};
</script>

<style>
.title {
  font-size: 24px;
  font-weight: bold;
}
</style>
