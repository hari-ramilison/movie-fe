<template>
  <main>
    <v-container>
      <v-row
        align="center"
        justify="center"
      >
        <v-col>
          <blockquote>
          Welcome {{validUserName}}
          </blockquote>
        </v-col>
      </v-row>
    </v-container>

    <v-container fluid fill-height>
      <v-row
        align="center"
        justify="center"
      >
        <v-col 
          cols="12"
            sm="10"
            md="8"
        >
          <v-card class="elevation-2">
            <v-container
              fluid
              grid-list-md
            >
              <v-row>
                <v-col>
                  <v-card>
                    <v-img
                      :src="require('@/assets/images/logo.JPG')" height="300px">
                    </v-img>
                    <v-card-actions>
                      <v-btn flat color="orange" @click="viewMovies">View Details</v-btn>
                    </v-card-actions>
                  </v-card>
                </v-col>
                <v-col>
                  <v-card>
                    
                  </v-card>
                </v-col>
                <v-col>
                  <v-card>

                  </v-card> 
                </v-col>
              </v-row>
            </v-container>
          </v-card>
        </v-col>
      </v-row>
    </v-container>
  </main>
</template>

<script>
  import router from '../router';

  export default {
    name: 'Home',
    data: () => ({
      validUserName: "Guest"
    }),
    mounted() {
      this.getUser();
    },
    methods: {
      viewMovies() {
        router.push('/movie-list');
      },
      getUser() {
        if (localStorage.getItem("isAuthenticates")
          && JSON.parse(localStorage.getItem("isAuthenticates")) === true) {
          this.validUserName = JSON.parse(localStorage.getItem("log_user"));
        }
      }
    }
  }
</script>
