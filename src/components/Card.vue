<template>
  <div>
    <div class="one row mb-2 g-0 border rounded overflow-hidden flex-md-row mb-4 shadow-sm h-md-250 position-relative">
      <div class="col p-4 d-flex flex-column position-static">
        <div class="blok_genres">
          <p class="card-text mb-auto">{{ list_genre }}</p>
        </div>
        <p class="card-text mb-auto">{{ getMarkName(movie_data.mark) }}</p>
        <p fl="">{{ movie_data.title }}</p>
        <div class="col-md-3 card">
          <b-img :src="`${$store.getters.getServerUrl}`+movie_data.poster"></b-img>
        </div>
        <div class="wrapper">
          <div class="info">
            <div class="mb-1 text-muted">{{ author }}</div>
            <p class="card-text mb-auto">{{ movie_data.description }}</p>
          </div>
          <button type="button" v-on:click="goTo()" class="btn btn-outline-danger btn-sm">Открыть
          </button>
        </div>
      </div>
    </div>
  </div>
</template>


<script>
import {mapActions} from "vuex";

export default {
  name: "Card",
  props: {
    movie_data: {
      type: Object,
      default() {
        return {}
      }
    }
  },
  created() {
    this.loadListGenre(),
        this.loadAuthor()
  },
  mounted() {
    this.loadListMarks()
  },
  methods: {
    ...mapActions([
      'loadListMarks',
      'getGenreFromAPI'
    ]),
    goTo() {
      this.$router.push({name: 'SingleView', params: {id: this.movie_data.id}})
    },
    loadListGenre() {
      for (let genre_i of this.movie_data.genres) {
        let genre = this.$store.state.genre.find(obj => obj.id == genre_i)
        this.list_genre = this.list_genre + String(genre.name) + ". "
      }
    },
    getMarkName(id) {
      let obj_mark = this.$store.getters.getMark(id);
      if (obj_mark != undefined) {
        return String(obj_mark.status) + "--" + String(obj_mark.value) + "б."
      }
    },
    async loadAuthor() {
      this.author = await fetch(
          `${this.$store.getters.getServerUrl}/username/${this.movie_data.user}`
      ).then(response => response.json()).catch((error) => {
        console.error('Ошибка:', error);
      })
    },

  },
  data() {
    return {
      list_genre: '',
      author: ''
    }
  }
}
</script>

<style>
</style>