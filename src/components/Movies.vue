<template>
  <section>
    <!-- cards movies -->
    <div class="card movie" v-for="movie, i in importMovieData" :key="i">
      
      <div>
        <img src="https://www.uilmtorino.it/wp-content/themes/consultix/images/no-image-found-360x260.png" alt="no image" v-if="movie.backdrop_path === null">
        <img :src="`https://image.tmdb.org/t/p/w342/${movie.backdrop_path}`" :alt="movie.title" v-else>
      </div>
      
      <ul>
        <li><span>Title: </span>{{movie.title}}</li>
        <li><span>Original Title: </span>{{movie.original_title}}</li>
        <li><span>Language: </span><img :src="require(`../assets/flags/${movie.original_language}.png`)" :alt="movie.original_language"></li>
        <li><span>Vote: </span>{{movie.vote_average}}</li>
        <li><span>Overview: </span> {{movie.overview}}</li>
      </ul>

      <div class="tag">Movie</div>
    </div>

    <!-- cards tv shows -->
    <div class="card tv" v-for="tv, i in importTvData" :key="'A'+ i">
      
      <div>
        <img src="https://www.uilmtorino.it/wp-content/themes/consultix/images/no-image-found-360x260.png" alt="no image" v-if="tv.backdrop_path === null">
        <img :src="`https://image.tmdb.org/t/p/w342/${tv.backdrop_path}`" :alt="tv.title" v-else>
      </div>
      
      <ul>
        <li><span>Title: </span>{{tv.name}}</li>
        <li><span>Original Title: </span>{{tv.original_name}}</li>
        <li><span>Language: </span><img :src="require(`../assets/flags/${tv.original_language}.png`)" :alt="tv.original_language"></li>
        <li><span>Vote: </span>{{tv.vote_average}}</li>
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
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
  section{
    display: flex;
    flex-wrap: wrap;
    padding: 20px 0;

    .card{
      max-width: 342px;
      margin: 5px 10px;
      height: 500px;
      overflow-y: auto;
      color: white;
      background-color: black;
      border: solid white 2px;
      position: relative;

      .tag{
        position: absolute;
        top: 5px;
        right: 5px;
        background-color: black;
        padding: 1px 2px;
        border-radius: 5px;
      }

      div {
        max-height: 178.52px;
        overflow: hidden;

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
      
        span {
          font-weight: 700;
        }
      }
    }
    
  }
</style>
