<template>
  <div class="home">
    <main class="main_page d-flex flex-nowrap">
      <Sidebar
          @filter="filterByGenre"/>
      <Catalog
          :listMovie="movie"/>
    </main>
  </div>
</template>

<script>

import Catalog from "@/components/Catalog";
import Header from "@/components/Header";
import Sidebar from "@/components/Sidebar";
import {toRaw} from "vue";

export default {
  name: 'HomeView',
  components: {
    Sidebar,
    Header,
    Catalog,
  },
  data() {
    return {
      allMovie: [],
      movie: [],
    }
  },
  created() {
    this.loadListMovie()
  },
  methods: {
    async loadListMovie() {
      this.movie = await fetch(
          `${this.$store.getters.getServerUrl}/movie`
      ).then(response => response.json()).catch((error) => {
        console.error('Ошибка:', error);
      })
      this.allMovie = this.movie
    },
    filterByGenre(genre) {
      this.movie = toRaw(this.movie)
      this.movie = this.allMovie.filter(function (item) {
        return item.genres.includes(genre)
      })
    }
  }
}

</script>

<style>
.home {
  background-image: url(../assets/images/back.jpg);
}

.main_page {
  margin-right: 15%;
}
</style>

