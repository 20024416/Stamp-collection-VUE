<template>
  <div id="app">
    <div id="container">
      <h1>My Stamp Collection</h1>
      <Pagination :total-pages="totalPages" :current-page="currentPage" @change-page="changePage"></Pagination>
      <StampTable :stamps="stampsToDisplay"></StampTable>
    </div>
  </div>
</template>

<script>
import StampTable from '../components/StampTable.vue';
import Pagination from '../components/Pagination.vue';
import axios from 'axios';

export default {
  name: 'App',
  components: {
    StampTable,
    Pagination
  },
  data() {
    return {
      stamps: [],
      itemsPerPage: 5,
      currentPage: 1
    }
  },
  computed: {
    stampsToDisplay() {
      const startIndex = (this.currentPage - 1) * this.itemsPerPage;
      const endIndex = startIndex + this.itemsPerPage;
      return this.stamps.slice(startIndex, endIndex);
    },
    totalPages() {
      return Math.ceil(this.stamps.length / this.itemsPerPage);
    }
  },
  methods: {
    changePage(page) {
      this.currentPage = page;
    }
  },
  created() {
    // axios.get('https://stampapp.azurewebsites.net:3001/stamps')
    // axios.get('http://localhost:3001/stamps')
    axios.get('https://my-json-server.typicode.com/20024416/dbStamps/stamps')
      .then(response => {
        this.stamps = response.data;
      })
      .catch(error => {
        console.log(error);
      });
  }
};
</script>

<style>
body {
  margin: 0;
  padding: 0;
  font-family: Arial, sans-serif;
  background-color: #f1f1f1;
}

.container {
  width: 100%;
  max-width: 1200px;
  margin: auto;
}

h1 {
  font-size: 2rem;
  text-align: center;
  color: #000000;
  margin-top: 1rem;
}

table {

  width: 80%;
  margin-left: auto;
  margin-right: auto;
}

th,
td {
  text-align: center;
  padding: 0.5rem;
  border: 1px solid #ddd;
  background-color: #333;
  color: #ddd;
}

th {
  background-color: #002b58;
  color: #fff;
}

button {
  background-color: #002b58;
  color: #fff;
  padding: 0.5rem 1rem;
  border: none;
  border-radius: 0.25rem;
  cursor: pointer;
  margin-bottom: 1rem;
}

button:hover {
  background-color: #0062cc;
}
</style>