<template>
  <div>
    <SearchBar v-model="query" @search="searchMovies" />
    <CarouselComponent />
    <div class="search-results movie-container" v-if="searchResults.length > 0">
      <div class="movie-container">
        <MovieCard v-for="movie in searchResults" :key="movie.id" :movie="movie"></MovieCard>
      </div>
      <PaginationComponent :totalPages="totalPages" :currentPage="currentPage" :onChangePage="changePage" />
    </div>
  </div>
</template>

<script>
import axios from 'axios';
//components
import MovieCard from './components/MovieCard.vue';
import SearchBar from './components/SearchBar.vue';
import PaginationComponent from './components/PaginationComponent.vue';
import CarouselComponent from './components/CarouselComponent.vue';

export default {
  components: {
    MovieCard,
    SearchBar,
    PaginationComponent,
    CarouselComponent // added here
  },
  data() {
    return {
      popularMovies: [], // Películas populares
      searchResults: [], // Películas obtenidas de la búsqueda
      query: '', // Query de búsqueda
      totalPages: 0, // Total de páginas
      currentPage: 1 // Página actual
    }
  },

  mounted() {
    // Llamada a la API al cargar el componente - carrusel,
    axios.get(`https://api.themoviedb.org/3/movie/popular?api_key=${process.env.VUE_APP_API_KEY}&language=es-ES&page=1`)
      .then(response => {
        console.log(response.data)
        this.popularMovies = response.data.results;
      })
      .catch(error => {
        console.log(error);
      });
  },
  methods: {
    searchMovies() {
      axios.get(`https://api.themoviedb.org/3/search/movie?api_key=${process.env.VUE_APP_API_KEY}&language=es-ES&query=${this.query}&page=1&include_adult=false`)
        .then(response => {
          console.log('has buscado: ' + this.query)
          this.totalPages = response.data.total_pages;
          this.currentPage = response.data.page;
          this.searchResults = response.data.results;
        })
        .catch(error => {
          console.log(error);
        });
    },
    onChangePage(pageNumber) {
      this.currentPage = pageNumber;
    }
  }
}
</script>

<style scoped>
.movie-container {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  margin-top: 2rem;
}

.movie-card {
  width: 400px;
  height: 560px;
  margin-bottom: 2rem;
  display: flex;
  justify-content: center;
  align-items: center;

  border-radius: 3.5px 3.5px 3.5px 3.5px;
}
</style>