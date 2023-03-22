<template>
  <div class="pagination">
    <button :disabled="currentPage === 1" @click="prevPage">Prev</button>
    <span>{{ currentPage }} / {{ totalPages }}</span>
    <button :disabled="currentPage === totalPages" @click="nextPage">Next</button>
  </div>
</template>


<script>
export default {
  name: 'Pagination',
  props: {
    totalPages: {
      type: Number,
      required: true
    },
    currentPage: {
      type: Number,
      required: true
    }
  },
  methods: {
    prevPage() {
      if (this.currentPage > 1) {
        this.$emit('change-page', this.currentPage - 1);
      }
    },
    nextPage() {
      if (this.currentPage < this.totalPages) {
        this.$emit('change-page', this.currentPage + 1);
      }
    }
  }
};
</script>

<style>
.pagination {
  display: flex;
  justify-content: center;
  align-items: center;
  margin: 2rem 0;
}

button {
  margin: 0 0.5rem;
}
</style>