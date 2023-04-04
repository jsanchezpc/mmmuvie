<template>
  <nav v-if="isMounted">
    <ul class="pagination">
      <li :class="{ disabled: page === 1 }">
        <a @click="changePage(currentPage - 1)" href="#" aria-label="Previous">
          <span aria-hidden="true">&laquo;</span>
        </a>
      </li>
      <li v-for="pageNumber in showPages" :key="pageNumber" :class="{ active: currentPage === pageNumber }">
        <a @click="changePage(pageNumber)" href="#">{{ pageNumber }}</a>
      </li>
      <li v-if="showPages[showPages.length - 1] !== totalPages - 1">
        <span>...</span>
      </li>
      <li v-if="showPages[showPages.length - 1] !== totalPages" :key="totalPages">
        <a @click="changePage(totalPages)" href="#">{{ totalPages }}</a>
      </li>
      <li :class="{ disabled: currentPage === totalPages }">
        <a @click="changePage(currentPage + 1)" href="#" aria-label="Next">
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
      isMounted: false,
      showPages: []
    }
  },
  mounted() {
    this.isMounted = true;
    this.updateShowPages();
  },
  watch: {
    currentPage() {
      this.updateShowPages();
    }
  },
  methods: {
    updateShowPages() {
      const pages = [];
      let startPage = Math.max(1, this.currentPage - 5);
      let endPage = Math.min(this.totalPages, this.currentPage + 5);
      if (startPage <= 10) {
        endPage = Math.min(this.totalPages, 20);
      } else if (endPage >= this.totalPages - 10) {
        startPage = Math.max(1, this.totalPages - 19);
      } else {
        pages.push(startPage - 1);
        endPage++;
      }
      for (let i = startPage; i <= endPage; i++) {
        pages.push(i);
      }
      this.showPages = pages;
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
  padding: 6px 12px;
  margin-left: -1px;
  line-height: 1.42857143;
  color: #337ab7;
  text-decoration: none;
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
</style>
  