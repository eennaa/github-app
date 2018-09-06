<template>
    <v-ons-page>
      <app-toolbar>
        <template slot="left"> </template>
        <template slot="right"> </template>    
      </app-toolbar>
      <app-search :query.sync="query" :placeholder="placeholder"></app-search>       
    </v-ons-page>
</template>
<script>
import AppToolbar from './components/AppToolbar.vue'
import AppSearch from './components/AppSearch.vue'
import debounce from 'lodash/debounce'
  export default{
    components: {
      AppToolbar,
      AppSearch
    },

    data() {
      return {
        query: "",
        placeholder: "Wnat someting?!"
      }
    },

    watch: {
      query: debounce((newValue) => {
        console.log(newValue)
      }, 500)
    }
  };
</script>
