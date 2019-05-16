<template>
<div>
    <MoviesDisplay :movies="movies" />
</div>
</template>

<script>
import MoviesDisplay from '@/components/Movies/MoviesDisplay.vue'

export default {
    watchQuery: ['page'],
    asyncData({ app, params, query, error }) {
        return app.$axios.$get('/api/v1/moviedb/movies/category/' + params.id, { 
                params: { 
                    page: query.page
                } 
            }).then(res => {
            return {
                movies: res
            }
        });
    },
    components: {
        MoviesDisplay,
    }
}
</script>
