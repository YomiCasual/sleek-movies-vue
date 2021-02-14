<template>
  <div className="movie-list">
     <div v-for="movie in movies" :key="movie.imdbID" class="movie-card"> 
        <router-link :to="'/movie/' + movie.imdbID">
        <div class="movie-link">
          <div class="product-image">
            <img :src="movie.Poster" alt="Movie_picture">
            <h5 class="movie-type">{{movie.Type}}</h5>
          </div>
          <div class="movie-content">
             <p>{{movie.Year}}</p>
            <h3>{{movie.Title}}</h3>
            
          </div>
        </div>
          
        </router-link>
        
     
     </div>
  </div>
</template>

<script>
export default {
  props: {
    movies: Array
  }
}
</script>

<style lang="scss">

.movie-list {
   display: flex;
   flex-wrap: wrap;
    margin: 0 8px;
    justify-content: center;

   .movie-card {
    max-width: 50%;
    padding: 10px 16px;
    width: 300px;
    
     
     .movie-link {
        display: flex;
        flex-direction: column;
        margin: 0!important;
        transition: 0.5s all ease;

        &:hover {
          box-shadow: 4px 8px 12px rgba(0,0,0,0.2);

          img {
            transform: scale(1.4)
          }
        }

        
        .product-image {
          position: relative;
          overflow: hidden;
          

           img {
              /* height: 250px; */
              /* transform: scale(1.03); */
              width: 100%;
              object-fit: cover;   
              transition: 0.5s all ease;
            }

        .movie-type {
          position: absolute;
          left: 0;
          bottom: 35px;
          background: #42b883;
          color: white;
          padding: 6px 8px;
          text-transform: capitalize;
          box-shadow: 4px 0px 8px rgba(0,0,0,0.2);
        }
     }

     .movie-content {
       padding: 1rem 0.7rem;
       color: #04182e;
       /* transform: translateY(-10px); */
       border-radius: 0 0 8px 8px;
       transition: 0.6s all ease;


       p {
         font-size: 14px;
         font-weight: bold;
       }
     }
     

     }

    
   }
   
}

</style>