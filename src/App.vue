<template>
    <v-ons-page>
      <app-toolbar>
        <template slot="left"> </template>
        <template slot="right"> </template>    
      </app-toolbar>
      <app-search :query.sync="query" :placeholder="placeholder"></app-search>
      <!-- {{ repos }}      -->
      <app-list-repos :repos="repos" 
                      :query="query"
                      :loadingRepos="loadingRepos"> </app-list-repos>
    </v-ons-page>
</template>
<script>
import AppToolbar from './components/AppToolbar.vue'
import AppSearch from './components/AppSearch.vue'
import AppListRepos from './components/AppListRepos.vue'
import debounce from 'lodash/debounce'
import { gitHub } from './services/GitHubService.js'

  export default{
    components: {
      AppToolbar,
      AppSearch,
      AppListRepos
    },

    data() {
      return {
        query: "",
        placeholder: "Wnat someting?!",
        repos: [],
        loadingRepos: false
      }
    },

    watch: {
      query: debounce(function (newValue) {
        // console.log(newValue)
        this.loadingRepos = true
        gitHub
        .getRepos(newValue)
        .then((response) => {
          this.repos = response.data
        })
        .catch( (error) => {console.log(error) })
        .finally((vm) => this.loadingRepos = false)
      }, 500)
    }
  };
</script>
