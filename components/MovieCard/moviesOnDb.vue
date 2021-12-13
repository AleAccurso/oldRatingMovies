<template>
  <div>
    <v-container class="grey lighten-5 mainLogo">
      <img src="../../assets/logo_big.png">
    </v-container>
    <v-container class="grey lighten-5 mainContainer">
        <v-row no-gutters>
            <v-col
                v-for="movie in movies" :key="movie.id"
                cols="12"
                sm="3"
            >
                <v-card
                    class="mx-auto"
                    max-width="300"
                    shaped
                >
                    <div class="hover10">
                        <figure>
                            <img class="w-100 h-auto imgMovieCard" :srcset="url+movie.poster" >
                            <v-rating v-if="isAuthenticated"
                                class="favoriteMovie"
                                hover
                                length="1"
                                size="54"
                                :empty-icon="emptyIcon"
                                :full-icon="fullIcon"
                                color="yellow darken-3"
                                background-color="grey darken-1"
                            ></v-rating>
                        </figure>
                    </div>
                    <div class="cardInfos">
                    <v-card-title v-if="movie.title.length > 25">{{ movie.title.substring(0,22) }}...</v-card-title>
                    <v-card-title v-else>{{ movie.title }}</v-card-title>
                    <v-card-actions class="pa-4">
                        <v-rating v-if="isAuthenticated"
                        background-color="red lighten-3"
                        color="red"
                        hover
                        length="5"
                        size="18"
                        :value= "movie.grade/2"
                        @input="rateMovie($event, movie._id)"
                    ></v-rating>
                    <v-rating v-else
                        background-color="red lighten-3"
                        color="red"
                        hover
                        length="5"
                        size="18"
                        :value= "movie.grade/2"
                        readonly
                    ></v-rating>
                    </v-card-actions>

                    <div class="my-3 text-subtitle-1">
                        <svg style="width:20px;height:20px;color:#9042b4;" viewBox="0 0 24 24">
                            <path fill="currentColor" d="M9,10H7V12H9V10M13,10H11V12H13V10M17,10H15V12H17V10M19,3H18V1H16V3H8V1H6V3H5C3.89,3 3,3.9 3,5V19A2,2 0 0,0 5,21H19A2,2 0 0,0 21,19V5A2,2 0 0,0 19,3M19,19H5V8H19V19Z" />
                        </svg>
                        {{ movie.date.substring(0,4) }}
                        </div>
                    <v-col
                        v-for="(item, i) in items"
                        :key="i"
                        cols="12"
                        >
                        <v-card
                            :color="item.color"
                            dark
                        >
                            <v-card-actions>
                                <v-btn
                                    color="orange lighten-2"
                                    text
                                >
                                    DESCRIPTION
                                </v-btn>

                                <v-spacer></v-spacer>

                                <v-btn
                                    icon
                                    @click="show = !show"
                                >
                                    <v-icon>{{ show ? 'mdi-chevron-up' : 'mdi-chevron-down' }}</v-icon>
                                </v-btn>
                            </v-card-actions>
                            <v-expand-transition>
                                <div v-show="show">
                                    <v-divider></v-divider>
                                    <v-card-text>
                                    <v-row
                                        align="center"
                                        class="mx-0"
                                    >
                                        <div>
                                        <p>{{ movie.overview }}</p>
                                        </div>
                                    </v-row>
                                    </v-card-text>
                                </div>
                            </v-expand-transition>
                            </v-card>
                    </v-col>
                    </div>
                </v-card>
            </v-col>
    </v-row>
    </v-container>
  </div>
</template>
<script>
    import axios from "axios";

  export default{
    data(){
      return {
        show: false,
        movieDbId: 0,
        title: '',
        genre: [],
        grade: 0,
        date: '',
        poster: '',
        director: '',
        overview: '',
        strGenre: '',
        url: 'http://image.tmdb.org/t/p/w500',
        movies: [],
        items: [
            {
            color: '#9042b4',
            },
        ],
        emptyIcon: 'mdi-heart-outline',
        fullIcon: 'mdi-heart',
        sortBy: 'title',
        sortDirection: 'asc',
        baseURL: process.env.baseURL
      }
    },
    computed: {
      isAuthenticated() {
        return this.$store.getters.isAuthenticated; // it check if user isAuthenticated
      },
    },
    methods: {
        rateMovie(value, id){
            axios
            .patch(
                this.baseURL +
                "/movies/" +
                id, {
                grade: value*2
            })
            .then(async (response) => {
                this.$store.commit('UPDATE_MOVIE',response.data);
            });
        },
    },
    created() {
        this.movies = this.$store.getters.getMovies;
    }
}
</script>
<style scoped>
.mainContainer{
    margin-top: 30px;
}
.mainLogo{
    margin-left:0;
    margin-right:0;
    text-align: center;
}
.mx-auto{
    margin-bottom: 40px;
}
.imgMovieCard {
  object-fit: cover;
  min-height: 450px;
  width: 100%;
  height: auto;
}
.v-card{
  margin: 10px 5px;
}
.v-card__text{
    max-height: 200px;
    overflow: scroll;
    font-family: 'Lato', sans-serif;
    font-size: 18px;
}
.v-card__title{
    padding: 16px 16px 0 16px;
    color: #9042b4;
    font-family: 'Ubuntu', sans-serif;
    font-weight: 600;
}
.text-subtitle-1{
    padding: 0 0 0 14px;
    font-family: 'Lato', sans-serif;
    font-weight: 600;
    color: #9042b4;
    font-size: 17px;
}
.cardInfos{
    background-color: #d29eeb31;
}
.mx-auto{
    min-height: 645px;
}
.v-card__actions{
    padding: 0 0 0 7px;
}
.v-sheet.v-card.v-sheet--shaped {
    border-radius: 14px 14px;
}
.imgMovieCard{
    min-height: 450px;
}
figure{
    margin: 0;
}
.favoriteMovie{
    font-size: 64px;
    position: absolute;
    top: -15px;
    right: 5px;
    color: #ffffff;
}
.v-icon.v-icon.v-icon--link {
    cursor: pointer;
    outline: none;
    color: #9042b4;
}

/* Blur + Gray Scale */
.hover10 figure img {
	-webkit-filter: sepia(0);
	filter: sepia(0);
	-webkit-transition: .6s ease-in-out;
	transition: .6s ease-in-out;
    border-top-left-radius: 14px;
    border-top-right-radius: 14px;
    cursor: pointer;
}
.hover10 figure:hover img {
	-webkit-filter: sepia(100%);
	filter: sepia(100%);
}
</style>
