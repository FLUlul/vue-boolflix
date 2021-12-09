<template>
  <section>

    <Cards
    :dataArray="movieData"
    :castArray="castMovieData"
    :Type="'Movie'"
    />

<!--     <Cards
    :dataArray="tvData"
    :castArray="castMovieData"
    :Type="'Series'"
    /> -->

  </section>
</template>

<script>
import axios from 'axios'
import Cards from '@/components/Cards.vue'

export default {
  
  name: 'Movies',

  components: {
    Cards,
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
      castMovieData: [],

      savedIDArr: [],
    }
  },
  /* "watch" works when "somethingToWatch" change do {that} */
  watch: {
    importInput(){

      this.savedIDArr = []
      this.castMovieData = []

      if (this.importInput !== '') {
        /* axios movies call */
        axios
        .get (this.urimovie + this.apikey + this.apiquery + this.importInput)
        .then ((result) => {
          this.movieData = result.data.results
          console.log(this.movieData);

          this.movieData.forEach((element, index) => {
            this.savedIDArr.push(element.id)
            console.log(this.savedIDArr);
            axios
            .get ('https://api.themoviedb.org/3/movie/' + this.savedIDArr[index] + '/credits' + this.apikey)
            .then ((result) => {
              if (result.data.cast.length > 5) {
                result.data.cast.length = 5
              }
              this.castMovieData.push(result.data.cast)
              console.log('cast-array:', this.castMovieData);
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
        /* axios
        .get (this.uritv + this.apikey + this.apiquery + this.importInput)
        .then ((result) => {
          this.tvData = result.data.results
        })
        .catch((error) => {
        console.log(error);
        }) */

      } 
    },
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">

</style>
