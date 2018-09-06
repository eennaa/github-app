<template>
  <v-ons-search-input :placeholder="placeholder" :value="query" @input="onInput">

  </v-ons-search-input>
</template>

<script>
export default {
  props: {
    query : {
      type: String
    },
    placeholder: {
      type: String,
      default: "You were searching for something?"
    }
  },

  methods: {
    onInput($event) {
      this.$emit('update:query', $event.target.value)
    }
  }
  
}
</script>