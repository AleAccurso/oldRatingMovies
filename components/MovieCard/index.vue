<template>
  <div>
    <div class="mt-4">
      <v-container class="grey lighten-5">
        <v-row>
            <v-col
                v-for="movie in getResult" :key="movie.id"
                cols="12"
                sm="3"
            >
                <v-card
                    class="mx-auto"
                    max-width="300"
                >
                <img class="w-100 h-auto" :srcset="url+movie.poster_path" >

                <v-card-title>{{ movie.title }}</v-card-title>
                <v-card-text>
                <v-row
                    align="center"
                    class="mx-0"
                >
                    <div class="my-3 text-subtitle-1">
                    {{ /[^-]*/.exec(movie.release_date)[0] }}
                    </div>
                    <div>
                    <p>{{ movie.overview }}</p>
                    </div>

                </v-row>
                </v-card-text>
                  <v-card-actions>
                    <button type="submit" @click="checkIsInDB(movie.id)" class="btn w-50 mb-2 registerButton">Add Movie</button>
                    <!-- <v-btn
                      class = "mx-2"
                      form="form"
                      color="deep-purple lighten-2"
                      text
                      @click="checkIsInDB(movie.id)"
                    >
                      Add Movie
                    </v-btn> -->
                  </v-card-actions>
                </v-card>
            </v-col>
        </v-row>
      </v-container>
    </div>
  </div>
</template>

<script>
  import axios from "axios";

  export default{
    data(){
      return {
        movieDbId: 0,
        movieToAdd: '',
        title: '',
        genre: [],
        grade: 0,
        date: '',
        poster: '',
        director: '',
        overview: '',
        strGenre: '',
        url: 'http://image.tmdb.org/t/p/w500',
        baseURL: process.env.baseURL
      }
    },
    computed :{
      getResult(){
          return this.$store.getters.getResult;
      },
    },
    methods:{
      checkIsInDB(id){
        let inDb = this.$store.getters.idInDb(id);
        if(inDb == "Add OK"){
          this.getInfo(id);
        }else{
          alert("Already in your database.");
        }
      },
      getInfo(id){
        axios
            .post(this.baseURL + "/movies/" + id + "/getInfo")
            .then(async(response) => {
              this.movieToAdd = response.data;
              this.addMovie();
            });
      },
      addMovie(){
        axios
            .post(this.baseURL + "/movies", this.movieToAdd)
            .then(async(response) => {
              await this.$store.commit('ADD_MOVIE', this.movieToAdd);
              alert ("Movie successfully added");
              this.$router.push("/admin");
        });
      }
    },
  }
</script>
