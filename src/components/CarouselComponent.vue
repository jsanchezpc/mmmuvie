<template>
  <div class="movies-carousel">
    <swiper-core :options="swiperOptions">
      <swiper-slide v-for="movie in movies" :key="movie.id">
        <img :src="`https://image.tmdb.org/t/p/w500${movie.poster_path}`" alt="">
      </swiper-slide>
    </swiper-core>
  </div>
  
</template>
  
<script>
import { SwiperSlide } from 'swiper/vue';
import SwiperCore, { Navigation, Pagination, Autoplay } from 'swiper/core';
import 'swiper/swiper-bundle.css';
import axios from 'axios';

SwiperCore.use([Navigation, Pagination, Autoplay]);

export default {

  components: {
    SwiperSlide,
    SwiperCore: SwiperCore.component // using SwiperCore as a component
  },
  data() {
    return {
      movies: [],
      swiperOptions: {
        slidesPerView: 3,
        spaceBetween: 30,
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
.movies-carousel {
  background: rgb(11, 36, 71);
  background: -moz-linear-gradient(left, rgba(11, 36, 71, 1) 0%, rgba(125, 185, 232, 1) 50%, rgba(11, 36, 71, 1) 100%);
  background: -webkit-linear-gradient(left, rgba(11, 36, 71, 1) 0%, rgba(125, 185, 232, 1) 50%, rgba(11, 36, 71, 1) 100%);
  background: linear-gradient(to right, rgba(11, 36, 71, 1) 0%, rgba(125, 185, 232, 1) 50%, rgba(11, 36, 71, 1) 100%);
  filter: progid:DXImageTransform.Microsoft.gradient(startColorstr='#0b2447', endColorstr='#0b2447', GradientType=1);
}


.swiper-slide {
  display: flex;
  justify-content: center;
}


.swiper-wrapper {
  display: flex;
  justify-content: center;
  width: 100%;
}
</style>
  