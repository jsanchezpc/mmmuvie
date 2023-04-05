<template>
    <div class="movie-card" @mouseenter="showDescription" @mouseleave="hideDescription">
      <h3 class="movie-title">{{ movie.original_title }}</h3>
      <img :src="getImageUrl(movie.poster_path)" :alt="movie.original_title" />
      <div class="description" :class="{ 'show': showDesc }">{{ movie.overview }}</div>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      movie: Object,
    },
    data() {
      return {
        showDesc: false,
        timeoutID: null,
      };
    },
    methods: {
      getImageUrl(path) {
        if (path === null) {
          return 'https://via.placeholder.com/500x750';
        } else {
          return `https://image.tmdb.org/t/p/w500/${path}`;
        }
      },
      showDescription() {
        this.timeoutID = setTimeout(() => {
          this.showDesc = true;
        }, 1000);
      },
      hideDescription() {
        if (this.timeoutID) {
          clearTimeout(this.timeoutID);
          this.timeoutID = null;
        }
        this.showDesc = false;
      },
    },
  };
  </script>
  
  <style scoped>
  .movie-card {
    position: relative;
    width: 400px;
    height: 600px;
    margin: 1rem;
    cursor: pointer;
    overflow: hidden;
  }

  .movie-title {
    position: absolute;
    border-radius: 3.5px 3.5px 0 0;
    top: 0;
    left: 0;
    width: 100%;
    padding: 1rem;
    box-sizing: border-box;
    background-color: rgba(0, 0, 0, 0.8);
    color: #fff;
    font-size: 1.5rem;
    line-height: 1.2;
    text-align: center;
    transform: translateY(-40%);
    transition: transform 0.3s ease-in-out;
  }
  
  .movie-card img {
    width: 100%;
    height: 100%;
    object-fit: cover;
  }
  
  .movie-card .description {
    position: absolute;
    bottom: 0;
    left: 0;
    width: 100%;
    padding: 1rem;
    box-sizing: border-box;
    background-color: rgba(0, 0, 0, 0.8);
    color: #fff;
    font-size: 1.5rem;
    line-height: 1.2;
    text-align: justify;
    transform: translateY(100%);
    transition: transform 0.3s ease-in-out;
    overflow: hidden;
  }
  
  .movie-card .description.show {
    transform: translateY(0%);
  }
  </style>
  