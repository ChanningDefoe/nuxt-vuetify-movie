<template>
<div>
  <v-layout
    row
    wrap
  >
    <v-flex
    v-for="movie in movies.results"
    :key="movie.id"
    xs6
    md3
    >
      <!-- Movie Card -->
      <v-card 
      hover
      nuxt
      color="dark darken-2" 
      class="white--text ma-3"
      :href="'/movies/view/' + movie.id"
      >
        <v-img
          :src='"https://image.tmdb.org/t/p/w500/" + movie.poster_path'
          contain
        >
        </v-img>
        <v-card-title>
          <div>
            <span class="movie-title">{{movie.title}}</span><br>
            <span class="release-date">{{movie.release_date}}</span><br>
          </div>
        </v-card-title>
      </v-card>
      <!-- /Movie Card -->
    </v-flex>
    </v-layout>
    <v-layout row wrap justify-center>
      <v-flex md6 xs12 v-if="paginate">
          <v-pagination
          v-model="currentPage"
          :length="pageCount"
          @input="next"
          ></v-pagination>
      </v-flex>
    </v-layout>
</div>
</template>

<script>
export default {
    props: {
      movies: {
        type: Object,
        default: {}
      },
      paginate: {
          type: Boolean,
          default: true
      }
    },
    data() {
        return {
            currentPage: this.movies.page
        }
    },
    methods: {
        next() {
            this.$router.push({query: {page: this.currentPage}})
            // this.$router.replace({params: {page: this.currentPage});
        }
    },
    computed: {
        // max pageCount of 1000
        pageCount: function () {
            if (this.movies.total_pages < 1000) {
                return this.movies.total_pages
            } else {
                return 1000;
            }
        }
    }
}
</script>

<style scoped>

.movie-title {
    font-size: 14px;
}
.release-date {
    font-size: 12px;
}

@media only screen and (max-width: 600px) {
    .movie-title {
        font-size: 12px !important;
    }
    .release-date {
        font-size: 8px !important;
    }
} 

</style>