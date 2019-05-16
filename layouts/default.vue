<template>
  <v-app dark>
    <!-- Sidebar -->
    <v-navigation-drawer
      v-model="drawer"
      fixed
      app
    >
      <!-- -vlist -->
      <v-list>
        <v-list-tile
          v-for="(item, i) in topLinks"
          :key="i"
          :to="item.to"
          router
          exact
        >
          <v-list-tile-action>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-tile-action>
          <v-list-tile-content>
            <v-list-tile-title v-text="item.title" />
          </v-list-tile-content>
        </v-list-tile>

        <!-- Categories Dropdown -->
        <v-list-group
          prepend-icon="local_movies"
          :value="false"
        >
          <template v-slot:activator>
            <v-list-tile>
              <v-list-tile-title>Movie Categories</v-list-tile-title>
            </v-list-tile>
          </template>

          <v-list-tile 
          v-for="genre in MovieGenres" 
          :key="genre.id"
          :to="'/movies/category/' + genre.id + '/popular'">
            <v-list-tile-title v-text="genre.name"></v-list-tile-title>
            <!-- <v-list-tile-action>
              <v-icon v-text="genre.name"></v-icon>
            </v-list-tile-action> -->
          </v-list-tile>

        </v-list-group>
        <!-- /Categories Dropdown -->
      </v-list>
      <!-- /v-list -->
    </v-navigation-drawer>
    <!-- /Sidebar -->
    <v-toolbar
      fixed
      app
    >
      <v-toolbar-side-icon @click="drawer = !drawer" />
      <v-toolbar-title v-text="title" />
      <v-spacer />
    </v-toolbar>
    <v-content>
      <v-container fluid>
        <nuxt />
      </v-container>
    </v-content>
    <v-footer
      app
    >
    <v-layout
      justify-center
      row
      wrap
    >
      <v-flex
        py-1
        text-xs-center
        white--text
        xs12
      >
        <span>
        <a href="https://github.com/ChanningDefoe" class="git">
          <i class="fab fa-github"></i>
        </a>
        </span>
      </v-flex>
    </v-layout>
  </v-footer>
  </v-app>
</template>

<script>
import MovieGenres from '~/assets/json/MovieGenres.json'
export default {
  components: {
    MovieGenres,
  },
  data() {
    return {
      MovieGenres: MovieGenres.genres,
      drawer: false,
      topLinks: [
        {
          icon: 'apps',
          title: 'Home',
          to: '/'
        }
      ],
      title: 'Nuxt Movies'
    }
  }
}
</script>

<style>
.git {
  color: #ffffff !important;
}
.git:hover {
  color: #4fc08d !important;
}
</style>
