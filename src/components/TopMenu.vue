<template>
    <header class="navbar">
      <h1 class="navbar__title" style="text-align: center;">mmmuvie</h1>
      <div class="navbar__user">
        <span id="nav-username">Jorge</span>
        <button class="navbar__toggle" @click="toggleMenu">
          <i class="fas fa-bars"></i>
        </button>
        <ul class="navbar__menu" v-if="showMenu">
          <li class="navbar__menuItem">Opción 1</li>
          <li class="navbar__menuItem">Opción 2</li>
          <li class="navbar__menuItem">Opción 3</li>
        </ul>
      </div>
    </header>
  </template>
  
  <script>
  export default {
    name: "TopMenu",
    props: {
      username: {
        type: String,
        required: true,
      },
    },
    data() {
      return {
        showMenu: false,
      };
    },
    methods: {
      toggleMenu() {
        this.showMenu = !this.showMenu;
      },
    },
  };
  </script>
  
  <style scoped>

  #nav-username {
    font-size: 2.5em;
  }
  .navbar {
    z-index: 1;
    display: flex;
    justify-content: space-between;
    align-items: center;
    background-color: black;
    color: white;
    padding: 1rem;
    position: fixed;
    top: 0;
    width: 100%;
  }
  
  .navbar__title {
    text-align: center;
  }
  
  .navbar__user {
    display: flex;
    align-items: center;
    position: relative;
  }
  
  .navbar__toggle {
    background-color: transparent;
    border: none;
    color: white;
    cursor: pointer;
    font-size: 1.5rem;
    margin-left: 1rem;
  }
  
  .navbar__menu {
    background-color: black;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.25);
    list-style: none;
    margin: 0;
    padding: 0;
    position: absolute;
    right: 0;
    top: 100%;
    z-index: 1;
  }
  
  .navbar__menuItem {
    padding: 1rem;
  }
  
  @media (max-width: 768px) {
    .navbar__menu {
      display: none;
    }
    .navbar__toggle {
      display: block;
    }
  }
  </style>
  