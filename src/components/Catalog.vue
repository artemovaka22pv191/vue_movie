<template>
  <b-container class="t">
    <Info/>
    <div class="catalog row mb-3">
      <Card
          v-for="movie in listMovie"
          :key="movie.id"
          v-bind:movie_data="movie"
      />
    </div>
  </b-container>
</template>

<script>

import Card from "@/components/Card";
import Info from "@/components/Info";
import {toRaw} from "vue";

export default {
  name: "Catalog",
  props: ["listMovie"],
  components: {
    Info,
    Card
  }
}
</script>

<style scoped>
.catalog {
  margin-top: 5%;
  margin-right: 10%;
}
</style>