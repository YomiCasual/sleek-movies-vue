<template>
  <div class="movie-detail">
    <div class="left-frame">
       <div class="movie-detail-section">
        <h3 class="movie-title">{{movieDetails.Title}}</h3>
        <p><span>{{movieDetails.Year}}</span> | 
        <span> Type:  {{movieDetails.Type}}</span>
        </p>  
    </div>
    <div class="movie-poster">
      <img :src="movieDetails.Poster" alt="Movie Poster">
    </div>
    </div>

    <div class="right-frame">
        <div class="movie-plot">
      <p>{{movieDetails.Plot}}</p>
    </div>
     <div class="movie-detail-others">
      <div class="section">
          <p>IMDB Rating</p>
          <h3>{{movieDetails.imdbRating}}</h3>
      </div>
      <div class="section">
          <p>IMDB Votes</p>
          <h3>{{movieDetails.imdbVotes}}</h3>
      </div>
    </div>

    <div class="movie-sections">
      <div class="movie-detail-section">
          <h3>Actors</h3>
          <p>{{movieDetails.Actors}}</p>
      </div>
        <div class="movie-detail-section">
          <h3>Genre</h3>
          <p>{{movieDetails.Genre}}</p>
      </div>
        <div class="movie-detail-section">
          <h3>Language</h3>
          <p>{{movieDetails.Language}}</p>
      </div>
    </div>
    </div>
   
    

   
  </div>
</template>

<script>
import { onBeforeMount, ref} from 'vue'
import { useRoute } from 'vue-router'
import env from '../env'
export default {
  setup() {
    const  route = useRoute()
    const  userRoute = ref(route.params.id)
    const movieDetails = ref({})

    onBeforeMount(() => {
      console.log(route.params.id)
      if (route.params.id) {
        fetch(`http://www.omdbapi.com/?apikey=${env.apiKey}&i=${userRoute.value}&plot=full`)
      .then(res => res.json())
      .then(data => {
        console.log(data)
        movieDetails.value = data})
      .catch(err => console.log(err))
      }

      else {
        console.log("No")
      }
     
    })

    return {
      movieDetails
    }

  
  }

}
</script>

<style scoped lang="scss">
  .movie-detail {
    padding: 0 4rem;
    padding-top: 5rem;
    padding-bottom: 2rem;

    .movie-detail-section {
      text-align: center;
      margin-bottom: 1rem;
       h3 {
         font-size: 24px;
         color: #319e6d;
         margin-bottom: 0.3rem;
       }

       .movie-title {
         font-size: 32px;
       }
       p {
         font-weight: bold;
       }
    }
    .movie-poster {
      display: flex;
      justify-content: center;
      margin-bottom: 1rem;

      img {
        height: 350px;
      }
    }

    .movie-plot {
      text-align: center;
      margin-bottom: 1rem;
      line-height: 22px;
      font-weight: 500;
    }

    .movie-detail-others {
      display: flex;
      margin-bottom: 1rem;

      .section {
        width: 50%;
        text-align: center;
        
        h3 {
          font-size: 32px
        }

        p {
          font-size: 14px
        }
      }
    }
  }

  $breakpoint-tablet: 768px;
    @media (min-width: $breakpoint-tablet) {
      .movie-detail {
        display: flex;
        align-items: center;
        flex-wrap: wrap;
      }

      .right-frame, .left-frame {
        width: 50%;
        padding: 20px;
      }

      .left-frame {
        img {
           height: 500px!important;
        }
       
      }
      .right-frame {
        text-align: left;
        display: flex;
        flex-direction: column;

        .movie-plot {
          text-align: left;
        }

        .movie-detail-others {
          .section {
            text-align: left;
          }
        }

        .movie-detail-section {
          text-align: left
        }
      }
    }
</style>