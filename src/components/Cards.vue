<template>
  <div id="cards">

    <div class="card" v-for="object, i in dataArray" :key="i">
      
      <div class="poster">
        <img src="https://hesolutions.com.pk/wp-content/uploads/2019/01/picture-not-available.jpg" alt="no image" v-if="object.poster_path === null">
        <img :src="`https://image.tmdb.org/t/p/w342/${object.poster_path}`" :alt="object.title || object.name" v-else>
      </div>
      
      <ul>
        <!-- title -->
        <li><span>Title: </span>{{object.title || object.name}}</li>
        <!-- original title -->
        <li><span>Original Title: </span>{{object.original_title || object.original_name}}</li>
        <!-- language -->
        <li><span>Language: </span><img :src="require(`../assets/flags/${changeFlag(object.original_language)}.png`)" :alt="object.original_language"></li>
        <!-- vote -->
        <li>
          <span>
            Vote: 
          </span>
          <span v-for="star, index in voteArr" :key="'B' + index">
            <i v-if="transformVote(object.vote_average) > index" class="fas fa-star"></i>
            <i v-else class="far fa-star"></i>
          </span>
        </li>
        <!-- overview -->
        <li><span>Overview: </span> {{object.overview}}</li>
        <!-- cast -->
        <li>{{object.id}}</li>
        <li class="actor" v-for="actor, j in castArray[i]" :key="j">

          <span>Cast: </span> {{actor.name}} {{i}}

          <span v-if="actor.profile_path === null">no photo</span>

          <img v-else :src="`https://image.tmdb.org/t/p/w45/${actor.profile_path}`" :alt="actor.name">

        </li>
      </ul>

      <div class="tag">{{Type}}</div>
    </div>

    
  </div>
</template>

<script>
export default {
  name: 'Cards',

  props: {
    dataArray: Array,
    castArray: Array,
    Type: String
  },

  data(){
    return {
      newVote: 0,
      voteArr: [1,2,3,4,5],
      apikey: '?api_key=8e1d397aa3a246f7489f89325ede261e',
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

  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
  @import '~@fortawesome/fontawesome-free/css/all.min.css';

  #cards{
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    padding: 20px 0;  
  }

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

</style>