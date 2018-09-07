<template>
  <v-ons-card>
      <div class="center">
      <img src="https://pbs.twimg.com/media/Bt5MoW0CIAE9Fda.jpg" alt="Onsen UI" style="width: 100%">
        
        There are no {{ type }} here  
        <!-- promeniti ovo na type, odnosno da ispisuje npr "There are no repos here" -->
      </div>      
    </v-ons-card>
</template>

<script>
import pluralize from 'pluralize'

export default {
  props: {
    query: String,
    type: String
  }
}
</script>
