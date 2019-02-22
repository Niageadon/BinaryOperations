<template>
  <v-app
      :dark="darkTheme">
    <v-toolbar  v-on:click="darkTheme = !darkTheme">
      <v-toolbar-title class="headline text-uppercase">
        <span>Binary</span>
        <span class="font-weight-light"> Operations</span>
      </v-toolbar-title>
    </v-toolbar>

    <v-content>
      <ContentPage/>
    </v-content>
  </v-app>
</template>

<script>


import ContentPage from "@/components/ContentPage";
export default {
  name: 'App',
  components: {
    ContentPage

  },
  data () {
    return {
      darkTheme: true
    }
  }
}
</script>
