<template>
    <div class="search-bar">
        <input type="text" v-model="value" @input="search" placeholder="Escribe para buscar" />
    </div>
</template>
  
<script>
export default {
    data() {
        return {
            searchQuery: '',
            value: ''
        }
    },
    watch: {
        searchQuery(newVal) {
            this.$emit('search', newVal);
            this.value = '';
        }
    },
    methods: {
        search() {
            this.$emit('update:modelValue', this.value);
            this.$emit('search');
        }
    }
}
</script>
  
<style>
.search-bar {
    display: flex;
    justify-content: center;
    margin: 2rem 0;
}

.search-bar input {
  padding: 0.5rem;
  border-radius: 4px;
  width: 800px;
  height: 100px;
  max-width: 500px;
  font-size: 2em;
  text-align: center;
  outline: none;
  transition: all 0.3s ease-in-out;
  border-radius: 100px 100px 100px 100px;
}

.search-bar input:focus {
  width: 100%;
  font-size: 3em;
  max-width: none;
  border-radius: 7px 7px 7px 7px;
  transition: all 2s ease-in-out;
}

.search-bar input:not(:focus) {
  padding: 0.5rem;
  border-radius: 4px;
  width: 800px;
  height: 80px;
  max-width: 500px;
  font-size: 2em;
  text-align: center;
  outline: none;
  transition: all 0.5s ease-in-out;
  border-radius: 100px 100px 100px 100px;
}




</style>
