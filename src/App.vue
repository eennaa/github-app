<template>
    <v-ons-page>
      <app-toolbar>
        <template slot="left"> </template>
        <template slot="right"> </template>    
      </app-toolbar>
      <app-search :query.sync="query" :placeholder="placeholder"></app-search>
      <!-- {{ repos }}      -->
    </v-ons-page>
</template>
<script>
import AppToolbar from './components/AppToolbar.vue'
import AppSearch from './components/AppSearch.vue'
import debounce from 'lodash/debounce'
import { gitHub } from './services/GitHubService.js'

  export default{
    components: {
      AppToolbar,
      AppSearch
    },

    data() {
      return {
        query: "",
        placeholder: "Wnat someting?!",
        repos: []
      }
    },

    watch: {
      query: debounce(function (newValue) {
        // console.log(newValue)
        gitHub
        .getRepos(newValue)
        .then((response) => {
          this.repos = response.data
        })
      }, 500)
    }
  };
</script>
