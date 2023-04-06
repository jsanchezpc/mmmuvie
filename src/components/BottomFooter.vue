<template>
    <footer class="bottom-footer">
      <div class="bottom-footer">
        <p >&copy; {{ currentYear }} Mmmuvie, colabora y forma una comunidad sana.</p>
      </div>
    </footer>
  </template>
  
  <script>
  export default {
    data() {
      return {
        currentYear: new Date().getFullYear()
      }
    }
  }
  </script>
  
  <style>
  .bottom-footer {
    background-color: #000000;
    padding: 20px 0;
    text-align: center;
    color: white;
    font-size: 1.6em;
    position: relative;
    bottom: 0;
    height: 1200px;
  }
  </style>
  