<template>
  <section>

    <Genres
    :genresArray="genreData"
    @changeIt="saveSelectValue"
    />

    <div class="cards">
      
      <div v-if="importInput === ''">
        <h2 class="title-top">Top Rated Movies</h2>
        <div class="cards">
          <Cards
          v-for="object, i in topRatedMovies" :key="'top' + i"
          :dataObject="object"
          :Type="'Movie'"
          />
        </div>
      </div>
      

      <Cards
      v-for="object, i in filteredMovieData" :key="'movie' + i"
      :dataObject="object"
      :Type="'Movie'"
      />

      <Cards
      v-for="object, i in filteredTvData" :key="'tv' + i"
      :dataObject="object"
      :Type="'Series'"
      />
    </div>
    
  </section>
</template>

<script>
import axios from 'axios'
import Cards from '@/components/Cards.vue'
import Genres from '@/components/Genres.vue'

export default {
  name: 'Main',

  components: {
    Cards,
    Genres
  },

  props: {
    importInput: String,
  },

  data(){
    return {
      urimovie: 'https://api.themoviedb.org/3/search/movie',
      uritv: 'https://api.themoviedb.org/3/search/tv',
      apikey: '?api_key=8e1d397aa3a246f7489f89325ede261e',
      apiquery: '&query=',

      movieData: [],
      tvData: [],

      genreData: [],
      genreIds: [],
      selectValue: 'All',

      topRatedMovies: [],
    }
  },
  created() {
    /* axios call to get all movie genres */
    axios
    .get ('https://api.themoviedb.org/3/genre/movie/list' + this.apikey)
    .then ((result) => {
      this.genreData = result.data.genres

      this.genreData.forEach(element => {
        this.genreIds.push(element.id)
      });
    })
    .catch((error) => {
    console.log(error);
    })

    /* axios call to get the top rated movies*/
    axios
    .get ('https://api.themoviedb.org/3/movie/top_rated' + this.apikey)
    .then ((result) => {
      this.topRatedMovies = result.data.results
    })
    .catch((error) => {
    console.log(error);
    })
  },

  computed: {
    filteredMovieData() {
      if (this.selectValue === "All"){
        return this.movieData
      } 
      return this.movieData.filter((item) => {
        return item.genre_ids.includes(this.selectValue)
      })
    },

    filteredTvData() {
      if (this.selectValue === "All"){
        return this.tvData
      } 
      return this.tvData.filter((item) => {
        return item.genre_ids.includes(this.selectValue)
      })
    }
  },

  methods: {
    saveSelectValue(selectValue){
      this.selectValue = selectValue
    }
  },

  /* "watch" works when "somethingToWatch" change do {that} */
  watch: {
    importInput(){

      if (this.importInput !== '') {
        /* axios movies call */
        axios
        .get (this.urimovie + this.apikey + this.apiquery + this.importInput)
        .then ((result) => {
          this.movieData = result.data.results
          
          /* axios cast for movies call */
          this.movieData.forEach((element) => {
            axios
            .get ('https://api.themoviedb.org/3/movie/' + element.id + '/credits' + this.apikey)
            .then ((result) => {
              
              if (result.data.cast.length > 5) {
                result.data.cast.length = 5
              }
              //the array cast is created inside the object movie
              //element.cast = result.data.cast;
              this.$set(element, 'cast', result.data.cast)
            })
            .catch((error) => {
            console.log(error);
            })
          })
        })
        .catch((error) => {
        console.log(error);
        })
        
        /* axios tv series call */
        axios
        .get (this.uritv + this.apikey + this.apiquery + this.importInput)
        .then ((result) => {
          this.tvData = result.data.results

          /* axios cast for tvshows call */
          this.tvData.forEach((element) => {
            axios
            .get ('https://api.themoviedb.org/3/tv/' + element.id + '/credits' + this.apikey)
            .then ((result) => {

              if (result.data.cast.length > 5) {
                result.data.cast.length = 5
              }
              //the array cast is inserted inside the object tv, creating a brand new key 'cast'
              //element.cast = result.data.cast;
              this.$set(element, 'cast', result.data.cast)
            })
            .catch((error) => {
            console.log(error);
            })
          })
        })
        .catch((error) => {
        console.log(error);
        })

      } 
    },
  },

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
  .cards{
    display: flex;
    justify-content: center;
    flex-wrap: wrap;
    padding: 20px 0;  
  }
  .title-top {
    text-align: center;
    color: red;
  }
</style>
