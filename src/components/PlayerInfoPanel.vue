<template>
  <v-card height="60" class="font-weight-light">
    <v-card-title >
      <h2 class="font-weight-light">{{ trackInfo.artist }} - {{ trackInfo.title }}</h2>
      <v-spacer></v-spacer>
      <h3 >{{ trackInfo.seek | minutes }}/{{ trackInfo.duration | minutes }}</h3>
    </v-card-title>    
  </v-card>
</template>

<script>
  export default {
    props: {
      trackInfo: Object
    },
  }
</script>