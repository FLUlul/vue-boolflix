<template>
  <section>
    <!-- cards movies -->
    <div class="card movie" v-for="movie, i in importMovieData" :key="i">
      
      <div>
        <img src="https://hesolutions.com.pk/wp-content/uploads/2019/01/picture-not-available.jpg" alt="no image" v-if="movie.poster_path === null">
        <img :src="`https://image.tmdb.org/t/p/w342/${movie.poster_path}`" :alt="movie.title" v-else>
      </div>
      
      <ul>
        <li><span>Title: </span>{{movie.title}}</li>
        <li><span>Original Title: </span>{{movie.original_title}}</li>
        <li><span>Language: </span><img :src="require(`../assets/flags/${changeFlag(movie.original_language)}.png`)" :alt="movie.original_language"></li>
                <li>
          <span>
            Vote: 
          </span>

          <span v-for="star, index in voteArr" :key="'B' + index" >

            <i v-if="transformVote(movie.vote_average) > index" class="fas fa-star"></i>
            <i v-else class="far fa-star"></i>
            
          </span>

        </li>
        <li><span>Overview: </span> {{movie.overview}}</li>
      </ul>

      <div class="tag">Movie</div>
    </div>

    <!-- cards tv shows -->
    <div class="card tv" v-for="tv, i in importTvData" :key="'A'+ i">
      
      <div class="poster">
        <img src="https://hesolutions.com.pk/wp-content/uploads/2019/01/picture-not-available.jpg" alt="no image" v-if="tv.poster_path === null">
        <img :src="`https://image.tmdb.org/t/p/w342/${tv.poster_path}`" :alt="tv.title" v-else>
      </div>
      
      <ul>
        <li><span>Title: </span>{{tv.name}}</li>
        <li><span>Original Title: </span>{{tv.original_name}}</li>
        <li><span>Language: </span><img :src="require(`../assets/flags/${changeFlag(tv.original_language)}.png`)" :alt="tv.original_language"></li>
        <li>
          <span>
            Vote: 
          </span>

          <span v-for="star, index in voteArr" :key="'B' + index" >

            <i v-if="transformVote(tv.vote_average) > index" class="fas fa-star"></i>
            <i v-else class="far fa-star"></i>
            
          </span>

        </li>
        <li><span>Overview: </span> {{tv.overview}}</li>
      </ul>

      <div class="tag">Series</div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'Movies',

  props: {
    importMovieData: Array,
    importTvData: Array,
  },

  data(){
    return {
      newVote: 0,
      voteArr: [1,2,3,4,5],
    }
  },

  methods: {
    changeFlag(flag){
      if(flag == 'it'){
        return "it"
      }else if(flag == 'en'){
        return "en"
      }else{
        return "eu"
      }
    },

    transformVote(vote){
      return parseInt(Math.round(this.newVote = vote / 2))
    },

  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
  @import '~@fortawesome/fontawesome-free/css/all.min.css';

  section{
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    padding: 20px 0;

    .card{
      max-width: 342px;
      margin: 5px 10px;
      color: white;
      background-color: black;
      border: solid white 2px;
      position: relative;
      overflow: hidden;

      .tag{
        position: absolute;
        top: 5px;
        right: 5px;
        background-color: black;
        padding: 1px 2px;
        border-radius: 5px;
      }

      .poster {
        height: 100%;
        display: flex;
        align-items: center;

        img{
        max-width: 100%;
        }
      } 
      
      &:hover ul{
          background-color: black;
          display: block;
        }

      ul{
        list-style: none;
        width: 100%;
        height: 100%;
        position: absolute;
        top: 0;
        left: 0;
        display: none;
        z-index: 10;
        padding: 10px;
        overflow-y: auto;
      
        span {
          font-weight: 700;
        }
      }
    }
    
  }
</style>
