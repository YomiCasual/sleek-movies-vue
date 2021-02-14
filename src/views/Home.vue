<template>
  <router-link to="/movie/tt0468569" > 
    <div class="featured-card">
    <img 
    class="featured-image"
    src= "../assets/darknight.jpg"
     
    alt="background_img"
    >
    <div class="featured-card-content">
      <h2>The Dark Knight</h2>
      <p>Set within a year after the events of Batman Begins, Batman, Lieutenant James Gordon, and new district attorney Harvey Dent successfully begin to round up the criminals that plague Gotham City until a mysterious and sadistic criminal mastermind known only as the Joker appears in Gotham
        </p>
    </div>
  </div>

     </router-link>

  <div>
    <SearchForm 
      @searchMovie="searchMovie"
      
     />
    <MovieList
    v-if="!loading"
    :movies="movies"
     />
    <div
    v-else
    >
      Loading..
    </div>
  </div>

</template>

<script>
import { ref, watch} from 'vue'
import MovieList from './components/MovieList'
import SearchForm from './components/SearchForm'
import env from '../env'


export default {
  components: {
    MovieList,
    SearchForm
  },
  setup() {

  const movies = ref([])
  const loading = ref(false)
   
   const searchMovie = (data) => {
      loading.value = true
      fetch(`http://www.omdbapi.com/?apikey=${env.apiKey}&s=${data}`)
      .then(res => res.json())
      .then(data => {    
        movies.value = data.Search
        localStorage.setItem("movies", JSON.stringify(data.Search))
        loading.value= false
        })
      .catch(err =>{
        console.log(err)
        loading.value = false
      }
       
       )
   }

   watch(() => {
     movies.value = JSON.parse(localStorage.getItem('movies')) || []
     loading.value = false

     console.log(loading.value)
   })
   
   return {
     searchMovie,
     movies,
     loading
   }
  }

}
</script>

<style scoped lang="scss">

.featured-card {
  position: relative;
  padding-top: 3rem;

  .featured-image {
    position: relative;
    width: 100%;
    height: 400px;
    object-fit: cover;
  }

  .featured-card-content {
    position: absolute;
    right: 0;
    left: 0;
    bottom: 4px;
    background-color: rgba(0,0,0,0.7);
    color: white;
    padding: 1rem 2rem;

    h2 {
      margin-bottom: 0.5rem;
      color: #42b883
    }
    
  }
}


$breakpoint-tablet: 768px;
    @media (min-width: $breakpoint-tablet) {

  .featured-image {
    height: 400px!important;
  }
		
	}

</style>
