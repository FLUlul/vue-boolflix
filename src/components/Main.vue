<template>
  <section>

    <Genres
    :genresArray="genreData"
    @changeIt="saveSelectValue"
    />

    <div id="cards">
      <Cards
      v-for="object, i in filteredMovieData" :key="'movie' + i"
      :dataObject="object"
      :Type="'Movie'"
      />

      <Cards
      v-for="object, i in tvData" :key="'tv' + i"
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
    }
  },
  created() {
    axios
    .get ('https://api.themoviedb.org/3/genre/movie/list' + this.apikey)
    .then ((result) => {
      this.genreData = result.data.genres
      console.log(this.genreData);

      this.genreData.forEach(element => {
        this.genreIds.push(element.id)
        console.log(this.genreIds);
      });
    })
    .catch((error) => {
    console.log(error);
    })
    
    return this.genreData
  },

  computed: {
    filteredMovieData() {
      if (this.selectValue === "All"){
        return this.movieData
      } 
      return this.movieData.filter((item) => {
        return item.genre_ids.includes(this.selectValue)
      })
    }
  },

  methods: {
    saveSelectValue(selectValue){
      this.selectValue = selectValue
      console.log(this.selectValue);

/*       this.movieData.forEach((element) => {
      }) */
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
  #cards{
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    padding: 20px 0;  
  }
</style>
