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
    }
  };
</script>
