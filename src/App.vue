<template>
  <TopMenu :username="'jorge'" />
  <div>
    <CarouselComponent />
    <hr>
    <SearchBar v-model="query" @search="searchMovies" />
    <div class="search-results movie-container" v-if="searchResults.length > 0">
      <h2 id="title-results">Resultados de la búsqueda</h2>
      <div class="movie-container">
        <MovieCard v-for="movie in searchResults" :key="movie.id" :movie="movie"></MovieCard>
      </div>
      <PaginationComponent :totalPages="totalPages" :currentPage="currentPage"
        :onChangePage="page => searchMovies(page)" />
    </div>
    <hr>
  </div>
  <BottomFooter />
</template>

<script>
import axios from 'axios';
//components
import TopMenu from './components/TopMenu.vue';
import BottomFooter from './components/BottomFooter.vue';
import MovieCard from './components/MovieCard.vue';
import SearchBar from './components/SearchBar.vue';
import PaginationComponent from './components/PaginationComponent.vue';
import CarouselComponent from './components/CarouselComponent.vue';

export default {
  components: {
    MovieCard,
    SearchBar,
    PaginationComponent,
    CarouselComponent,
    TopMenu,
    BottomFooter
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
    axios.get(`https://api.themoviedb.org/3/movie/popular?api_key=${process.env.VUE_APP_API_KEY}&language=es-ES&page=${this.currentPage}`)
      .then(response => {
        console.log(response.data)
        this.popularMovies = response.data.results;
      })
      .catch(error => {
        console.log(error);
      });
  },
  methods: {
    searchMovies(page = 1) {
      axios.get(`https://api.themoviedb.org/3/search/movie?api_key=${process.env.VUE_APP_API_KEY}&language=es-ES&query=${this.query}&page=${page}&include_adult=false`)
        .then(response => {
          console.log('has buscado: ' + this.query)
          this.totalPages = response.data.total_pages;
          this.currentPage = response.data.page;
          this.searchResults = response.data.results;
        })
        .catch(error => {
          console.log(error);
        });
    }
    ,
    onChangePage(page) {
      this.currentPage = page;
      this.searchMovies();
    }
  }
}
</script>

<style scoped>
#title-results {
  text-align: center;
  font-size: 2.5em;
  margin: 2rem 0;
}

hr {
  margin: 2rem 0;
  border: 1px;
  border-top: 1px solid rgba(0, 0, 0, 0.1);

}

.movie-container {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  margin-top: 2rem;
  display: inlijne-block;
  justify-content: center;
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