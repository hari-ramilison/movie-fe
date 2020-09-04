<template>
  <v-app>
    <v-app-bar app color="green">
      <v-toolbar-title >My Favorite Movies</v-toolbar-title>
      <v-spacer></v-spacer>
      <v-btn flat dark @click="goHome" text rounded>Home</v-btn>
      <v-btn flat dark @click="viewMovies" text rounded>Movies</v-btn>
      <v-btn flat dark text rounded v-if="!authenticated"
              @click="login">Log in
      </v-btn>
      <v-btn flat dark text rounded v-if="authenticated"
              @click="logout">Log Out
      </v-btn>
    </v-app-bar>
    <v-content>
      <router-view/>
    </v-content>
  </v-app>

</template>

<script>
  import router from './router';
  import {APIService} from './http/APIService';
  const apiService = new APIService();

  export default {
    name: 'App',
    data: () => ({
      authenticated: false,
      dialog: false,
    }),

    mounted() {
      apiService.getMovieList().then(response => {
        this.authenticated = true;
      }).catch(error => {
        if (error.response.status === 401) {
          localStorage.removeItem('isAuthenticates');
          localStorage.removeItem('log_user');
          localStorage.removeItem('token');
          this.authenticated = false;
        }
      });
      console.log('this.authenticated--'+this.authenticated);
    },

    methods: {
      logout() {
        localStorage.removeItem('isAuthenticates');
        localStorage.removeItem('log_user');
        localStorage.removeItem('token');
        this.authenticated = false;
        // router.push('/');
        window.location = "/"
      },
      viewMovies() {
        router.push('/movie-list');
      },

     

      login() {
        router.push("/auth");
      },

      goHome() {
        router.push('/');
      }
    }
  };

</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>