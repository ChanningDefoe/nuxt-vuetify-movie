<template>
<div>
  <MoviesDisplay :movies='featured' :paginate='false' />
</div>
</template>

<script>
import MoviesDisplay from '@/components/Movies/MoviesDisplay.vue'

export default {
  head () {
    return {
      title: 'Home',
      meta: [
        { hid: 'description', name: 'description', 
        content: 'A Nuxt.js application for displaying movies from The Movie Database (TMDb) API.' }
      ]
    }
  },
  layout: "movies",
  asyncData({ app, params, query, error }) {
      return app.$axios.$get('/api/v1/moviedb/movies/trending')
      .then(res => {
            return {
              featured: res
            }
      })
  },
  components: {
    MoviesDisplay,
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