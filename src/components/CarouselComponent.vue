<template>
  <div class="movies-carousel">
    <h1 class="carousel-title">Películas populares</h1>
    <swiper :breakpoints="{ 700:{ slidesPerView:1 }, 1221:{ slidesPerView:3 }, 1641: { slidesPerView: 4} }" :slides-per-view="1" :speed=1000 :space-between="1" :options="swiperOptions">
      <SwiperSlide v-for="movie in movies" :key="movie.id">
        <div class="movie-container">
          <MovieCard :key="movie.id" :movie="movie"></MovieCard>
        </div>
      </SwiperSlide>
    </swiper>
  </div>
</template>
  
<script>
import { SwiperSlide, Swiper } from 'swiper/vue';
import SwiperCore, { Navigation, Pagination, Autoplay } from 'swiper/core';
import 'swiper/swiper-bundle.css';
import axios from 'axios';
import MovieCard from './MovieCard.vue';

SwiperCore.use([Navigation, Pagination, Autoplay]);

export default {

  components: {
    SwiperSlide,
    Swiper,
    MovieCard
  },
  data() {
    return {
      movies: [],
      modules: [Navigation, Pagination, Autoplay],
      swiperOptions: {
        navigation: true,
        pagination: {
          clickable: true,
          centeredSlides: true // Mover a las opciones de paginación
        },
        autoplay: {
          delay: 1000
        }
      },
    }
  },
  mounted() {
    axios.get(`https://api.themoviedb.org/3/movie/popular?api_key=${process.env.VUE_APP_API_KEY}&language=es-ES&page=1`)
      .then(response => {
        this.movies = response.data.results;
      })
      .catch(error => {
        console.log(error);
      });
  }
}
</script>
  
<style scoped>

.carousel-title {
  color: white;
  font-size: 3rem;
  font-weight: 600;
  margin-left: 50px;
  margin-top: 20px;
}


.movies-carousel {
  margin-top:114px;

  border-top-style: solid;
  border-top-width: 18px;
  border-top-left-radius: 20px;
  border-top-right-radius: 20px;
  border-top-color: rgba(0, 0, 0, 0.3);
  border-bottom-style: solid;
  border-bottom-width: 18px;
  border-bottom-left-radius: 20px;
  border-bottom-right-radius: 20px;
  border-bottom-color: rgb(0, 0, 0, 0.35);

  border-right-style: solid;
  border-right-width: 2px;
  border-right-color: rgba(85, 85, 85, 0.1);

  border-left-style: solid;
  border-left-width: 2px;
  border-left-color: rgba(85, 85, 85, 0.1);
  
  background: rgb(11, 36, 71);
  background: -moz-linear-gradient(left, rgba(11, 36, 71, 1) 0%, rgba(125, 185, 232, 1) 50%, rgba(11, 36, 71, 1) 100%);
  background: -webkit-linear-gradient(left, rgba(11, 36, 71, 1) 0%, rgba(125, 185, 232, 1) 50%, rgba(11, 36, 71, 1) 100%);
  background: linear-gradient(to right, rgba(11, 36, 71, 1) 0%, rgba(125, 185, 232, 1) 50%, rgba(11, 36, 71, 1) 100%);
  filter: progid:DXImageTransform.Microsoft.gradient(startColorstr='#0b2447', endColorstr='#0b2447', GradientType=1);
}


.swiper-slide {
  display: flex;
  justify-content: center;
  overflow: hidden;
}



.swiper-wrapper {
  display: flex;
  justify-content: center;
  width: 100%;
}

.description {
  position: absolute;
  bottom: 0;
  left: 0;
  width: 100%;
  padding: 1rem;
  box-sizing: border-box;
  background-color: rgba(0, 0, 0, 0.8);
  color: #fff;
  font-size: 1rem;
  line-height: 1.2;
  text-align: justify;
  transform: translateY(100%);
  transition: transform 0.3s ease-in-out;
}

.description.show {
  transform: translateY(0%);
}
</style>
  