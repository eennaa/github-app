<template>
  <v-ons-list>
    <v-ons-list-header>Repositories of {{ query }}</v-ons-list-header>
    <v-ons-list-item v-for="(repo, key) in repos" :key="key">
      {{ repo.name }}
      <!-- {{ repo. }} -->
      
    </v-ons-list-item>
  </v-ons-list>
</template>

<script>
export default {
  props: {
    query: String,
    repos: Array,
  }
}
</script>
