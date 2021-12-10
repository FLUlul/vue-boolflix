<template>
  <div class="card-container">
    
    <div class="poster">
      <img src="https://hesolutions.com.pk/wp-content/uploads/2019/01/picture-not-available.jpg" alt="no image" v-if="dataObject.poster_path === null">
      <img :src="`https://image.tmdb.org/t/p/w342/${dataObject.poster_path}`" :alt="dataObject.title || dataObject.name" v-else>
    </div>
    
    <ul>
      <!-- title -->
      <li><span>Title: </span>{{dataObject.title || dataObject.name}}</li>
      <!-- original title -->
      <li><span>Original Title: </span>{{dataObject.original_title || dataObject.original_name}}</li>
      <!-- language -->
      <li><span>Language: </span><img :src="require(`../assets/flags/${changeFlag(dataObject.original_language)}.png`)" :alt="dataObject.original_language"></li>
      <!-- vote -->
      <li>
        <span>
          Vote: 
        </span>
        <span v-for="star, index in voteArr" :key="'B' + index">
          <i v-if="transformVote(dataObject.vote_average) > index" class="fas fa-star"></i>
          <i v-else class="far fa-star"></i>
        </span>
      </li>
      <!-- overview -->
      <li><span>Overview: </span> {{dataObject.overview}}</li>
      <!-- cast -->
      <li><span>Cast: </span></li>
      <li class="actors">

        <div v-for="actor, j in dataObject.cast" :key="j">

          <span v-if="actor.profile_path === null"></span>

          <img v-else :src="`https://image.tmdb.org/t/p/w45/${actor.profile_path}`" :alt="actor.name">

          <span>{{actor.name}}</span>

        </div>

      </li>
    </ul>

    <div class="tag">{{Type}}</div>
    
  </div>
</template>

<script>
export default {
  name: 'Cards',

  props: {
    dataObject: Object,
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

  .card-container{
    max-width: 342px;
    margin: 5px 10px;
    color: white;
    background-color: black;
    border: solid white 1px;
    border-radius: 5px;
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

      li{
        margin: 5px 0;
      }

      .actors{
        display: flex;

        div{
          width: calc(100% / 5);
          text-align: center;

          span{
            overflow-wrap: break-word;
          }
        }
      }
  
      span {
        font-weight: 700;
      }
    }
  }

</style>