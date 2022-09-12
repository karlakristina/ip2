<template>
    <v-app id="inspire">
      <v-app-bar
        app
        shrink-on-scroll
      >
        <v-app-bar-nav-icon></v-app-bar-nav-icon>
  
        <v-toolbar-title>Application</v-toolbar-title>
  
        <v-spacer></v-spacer>
  
        <v-btn icon>
          <v-icon>mdi-dots-vertical</v-icon>
        </v-btn>
      </v-app-bar>
  
      <v-main>
        <v-container>
          <v-row>
            <v-col
              v-for="n in 24"
              :key="n"
              cols="4"
            >
              <v-card height="200"></v-card>
            
            </v-col>
          </v-row>
        </v-container>
      </v-main>
    </v-app>
  </template>
  
  <script>
  // @ is an alias to /src
  /*import HelloWorld from '@/components/HelloWorld.vue'*/
  export default {
    name: 'HomeView',
   
   
   data(){
    return {
      test: 'Test' ,
      movies:[]
    }
   },
    methods: {
      getData() {
        let api = "https://api.nytimes.com/svc/movies/v2/reviews/search.json"
        this.axios.get(api, {
          params:{
            "api-key": "Qy1ZLVjLaIhakGdt23JNT9RBgTg4FV7J"
          }
        }) .then((response) => {
          console.log(response.data)
        })
      }}
  }
  </script>