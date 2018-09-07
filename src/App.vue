<template>
    <v-ons-page>
      <app-toolbar>
        <template slot="left"> </template>
        <template slot="right"> </template>    
      </app-toolbar>
      <app-search :query.sync="query" :placeholder="placeholder"></app-search>
      <!-- {{ repos }}      -->
      <app-list-repos  v-show="query"
                      :repos="repos"
                      :query="query"
                      :loadingRepos="loadingRepos" />
      <empty-state v-show="noRepos"/> 

    </v-ons-page>
</template>
<script>
import AppToolbar from './components/AppToolbar.vue'
import AppSearch from './components/AppSearch.vue'
import AppListRepos from './components/AppListRepos.vue'
import EmptyState from './components/EmptyState.vue'

import debounce from 'lodash/debounce'
import { gitHub } from './services/GitHubService.js'

  export default{
    components: {
      AppToolbar,
      AppSearch,
      AppListRepos,
      EmptyState
    },

    data() {
      return {
        query: "",
        placeholder: "Want someting?!",
        repos: [],
        loadingRepos: false,
        noRepos: false
      }
    },

    watch: {
      query: debounce(function (newValue) {
        // console.log(newValue)
        this.loadingRepos = true
        this.noRepos = 0
        gitHub
        .getRepos(newValue)
        .then((response) => {
          this.repos = response.data
          
        })
        .catch( (error) => { if(error.response.status === 404){
                                  // dodaj ovde
                                } 
                          })
                            
        .finally((vm) => { this.loadingRepos = false })
      }, 500)
    }
  };
</script>
