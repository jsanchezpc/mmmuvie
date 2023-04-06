<template>
  <nav v-if="totalPages > 1">
    <ul class="pagination">
      <li :class="{ disabled: currentPage === 1 }">
        <a @click="onChangePage(currentPage - 1)" href="#" aria-label="Previous">
          <span aria-hidden="true">&laquo;</span>
        </a>
      </li>
      <li v-for="(pageNumber, index) in totalPagesArray" :key="index" :class="{ active: currentPage === pageNumber }">
        <a @click="onChangePage(pageNumber)" href="#">{{ pageNumber }}</a>
      </li>
      <li v-if="totalPagesArray[totalPagesArray.length - 1] < totalPages - 1">
        <span>...</span>
      </li>
      <li v-if="totalPagesArray[totalPagesArray.length - 1] < totalPages" :key="totalPages">
        <a @click="onChangePage(totalPages)" href="#">{{ totalPages }}</a>
      </li>
      <li :class="{ disabled: currentPage === totalPages }">
        <a @click="onChangePage(currentPage + 1)" href="#" aria-label="Next">
          <span aria-hidden="true">&raquo;</span>
        </a>
      </li>
    </ul>
  </nav>
</template>

<script>
export default {
  props: {
    currentPage: {
      type: Number,
      required: true
    },
    totalPages: {
      type: Number,
      required: true
    },
    onChangePage: {
      type: Function,
      required: true
    }
  },
  data() {
    return {
      totalPagesArray: []
    }
  },
  mounted() {
    this.changePage();
  },
  watch: {
    currentPage() {
      this.changePage();
    },
    totalPages() {
      this.changePage();
    }
  },
  methods: {
    changePage() {
      let startPage = Math.max(1, this.currentPage - 4);
      let endPage = Math.min(this.totalPages, this.currentPage + 4);

      if (endPage === this.totalPages) {
        startPage = Math.max(1, this.totalPages - 8);
      }

      this.totalPagesArray = [];

      for (let i = startPage; i <= endPage; i++) {
        this.totalPagesArray.push(i);
      }
    }
  }

}
</script>


  
<style>
.pagination {
  display: inline-block;
  padding-left: 0;
  margin: 20px 0;
  border-radius: 4px;
}

.pagination>li {
  display: inline;
}

.pagination>li>a,
.pagination>li>span {
  position: relative;
  float: left;
  padding: 20px 20px;
  margin-left: -1px;
  line-height: 1.42857143;
  color: #337ab7;
  text-decoration: none;
  font-size: 20px;
  font-weight: bold;
  background-color: #fff;
  border: 1px solid #ddd;
}

.pagination>li:first-child>a,
.pagination>li:first-child>span {
  margin-left: 0;
  border-top-left-radius: 4px;
  border-bottom-left-radius: 4px;
}

.pagination>li:last-child>a,
.pagination>li:last-child>span {
  border-top-right-radius: 4px;
  border-bottom-right-radius: 4px;
}

.pagination>.active>a,
.pagination>.active>span,
.pagination>.active>a:hover,
.pagination>.active>span:hover,
.pagination>.active>a:focus,
.pagination>.active>span:focus {
  z-index: 2;
  color: #fff;
  cursor: default;
  background-color: #337ab7;
  border-color: #337ab7;
}

.pagination>.disabled>span,
.pagination>.disabled>span:hover,
.pagination>.disabled>span:focus,
.pagination>.disabled>a,
.pagination>.disabled>a:hover,
.pagination>.disabled>a:focus {
  color: #777;
  cursor: not-allowed;
  background-color: #fff;
  border-color: #ddd;
}

.pagination .ellipsis {
  padding: 20px 10px;
  font-size: 20px;
  font-weight: bold;
  color: #337ab7;
}

@media (max-width: 576px) {

  .pagination>li>a,
  .pagination>li>span {
    padding: 10px;
    font-size: 14px;
  }

  .pagination .ellipsis {
    padding: 10px;
    font-size: 14px;
  }
}
</style>

  