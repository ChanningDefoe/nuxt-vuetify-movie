<template>
<div>
<v-container >
    <v-layout row wrap>
        <v-flex md4 xs12 px-2>
            <v-img 
            contain
            class="img-fluid" 
            :src='"https://image.tmdb.org/t/p/w500/" + movie.poster_path' />
        </v-flex>
        <v-flex md8 xs12 px-2>
            <h1 class="movie-title mb-0">{{movie.title}}</h1>
            <h2 v-if="movie.tagline" class="colorgreen text-uppercase tagline mb-0">{{movie.tagline}}</h2>
            <div class="mt-2">
                <span class="mr-2" v-if="movie.release_date">
                    <i class="far fa-calendar-alt fa-lg mr-2 colorgreen"></i> {{movie.release_date}}
                </span>
                <span v-if="movie.vote_average">
                    <i class="fas fa-star colorgreen"></i> {{movie.vote_average}}
                </span>
            </div>
            <div class="my-2">
                <v-btn
                v-for="genre in movie.genres"
                :key="genre.id"
                small 
                color="#4fc08d" 
                class="ml-0"
                :href='"/movies/category/" + genre.id + "/popular"'>
                {{genre.name}} 
                </v-btn>
            </div>
            <h3>Overview:</h3>
            <p>{{movie.overview}}</p>
        </v-flex>
    </v-layout>
</v-container>
</div>
</template>

<script>
export default {
    head () {
        return {
        title: this.movie.title,
        meta: [
            { hid: 'description', name: 'description', content: this.movie.title + ' | ' + this.movie.overview }
        ]
        }
    },
    asyncData({ app, params, query, error }) {
        return app.$axios.$get('/api/v1/moviedb/movies/info/' + params.id)
        .then(res => {
            return {
                movie: res
            }
        });
    }
}
</script>

<style scoped>
.movie-title {
    font-size: 45px;
}

.tagline {
    font-size: 18px;
}

@media only screen and (max-width: 600px) {
    .movie-title {
        font-size: 28px !important;
    }
}

.colorgreen {
    color: #4fc08d !important;
}
</style>