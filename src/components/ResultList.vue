<template>
  <div class="result-list">
    <h1>List of results</h1>

    <div v-if="loading" class="loading">
      Loading...
    </div>

    <div v-if="error" class="error">
      {{ error }}
    </div>

    <div v-if="results" class="content">
      <ResultItem
        v-for="data in results"
        v-bind:data="data"
        v-bind:key="data.id"
      />
    </div>
  </div>
</template>

<script>
import ResultItem from "./ResultItem.vue";

export default {
  name: "ResultList",
  components: {
    ResultItem,
  },
  data() {
    return {
      loading: false,
      results: null,
      error: null,
    };
  },
  created() {
    // Fetch the data when the view is created and the data is
    // already being observed. This approach is from:
    // https://router.vuejs.org/guide/advanced/data-fetching.html
    this.fetchData();
  },
  methods: {
    fetchData() {
      this.error = this.post = null;
      this.loading = true;

      // Fetch some dummy data for now.
      fetch("https://jsonplaceholder.typicode.com/todos")
        .then((res) => res.json())
        .then((out) => {
          this.loading = false;
          this.results = out.slice(0, 10);
        })
        .catch((err) => {
          this.loading = false;
          this.error = err;
          console.error(err);
        });
    },
  },
};
</script>
