<template>
    <div class="search-bar">
        <input type="text" v-model="value" @input="search" placeholder="Search movies..." />
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
    border: 1px solid #ccc;
    border-radius: 4px;
    width: 100%;
    max-width: 500px;
}
</style>
