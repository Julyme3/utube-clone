<template>
  <div class="flex w-full mr-2">
    <div class="relative flex w-full">
      <TheSearchInput
        v-model:query="query"
        :has-results="results.length"
        @update:query="updateSearchResults"
        @change-state="toggleSearchResults"
        @keyup.up="handlePreviousSearchResult"
        @keyup.down="handleNextSearchResult"
        @keydown.up.prevent
      />
      <TheSearchResults
        v-show="isSearchResultsShown"
        :results="results"
        :activeResultId="activeSearchResultId"
        @search-result-mouseenter="activeSearchResultId = $event"
        @search-result-mouseleave="activeSearchResultId = null"
        @search-result-click="selectSearchResult"
      />
    </div>
    <TheSearchButton />
  </div>
</template>

<script>
import TheSearchInput from './TheSearchInput.vue';
import TheSearchButton from './TheSearchButton.vue';
import TheSearchResults from './TheSearchResults.vue';
export default {
  name: 'TheSearch',
  components: { TheSearchResults, TheSearchButton, TheSearchInput },
  props: ['searchQuery'],
  emits: ['update-search-query'],
  data() {
    return {
      activeQuery: this.searchQuery,
      query: this.searchQuery,
      results: [],
      activeSearchResultId: null,
      keywords: [
        'new york giants',
        'new york alicia keys',
        'new york giants vs washington football',
        'new york',
        'new york song',
        'new york new york frank sinatra',
        'new york jets',
        'new york city',
        'new york giants live',
        'new york state of mind',
        'new york giants vs washington football live',
        'new york giants injury',
        'new york giants live stream',
        'new york accent',
      ],
      isSearchResultsShown: false,
    };
  },
  mounted() {
    document.addEventListener('click', this.handleClick);
  },
  beforeUnmount() {
    document.removeEventListener('click', this.handleClick);
  },
  computed: {
    trimmedQuery() {
      return this.query.replace(/\s+/g, ' ');
    },
  },
  methods: {
    updateSearchResults() {
      this.activeSearchResultId = null;
      this.activeQuery = this.query;

      if (!this.query) {
        return [];
      }

      this.results = this.keywords.filter((result) => {
        return result.includes(this.trimmedQuery);
      });
    },
    toggleSearchResults(isSearchInputActive) {
      this.isSearchResultsShown = isSearchInputActive && this.results.length;
    },
    handlePreviousSearchResult() {
      if (!this.isSearchResultsShown) {
        this.toggleSearchResults(true);
      } else {
        this.makePreviousSearchResultActive();
      }
    },
    handleNextSearchResult() {
      if (!this.isSearchResultsShown) {
        this.toggleSearchResults(true);
      } else {
        this.makeNextSearchResultActive();
      }
    },
    makePreviousSearchResultActive() {
      if (this.activeSearchResultId === null) {
        this.activeSearchResultId = this.results.length - 1;
      } else if (this.activeSearchResultId === 0) {
        this.activeSearchResultId = null;
      } else {
        this.activeSearchResultId--;
      }

      this.updateQueryWithSearchResult();
    },
    makeNextSearchResultActive() {
      if (this.activeSearchResultId === null) {
        this.activeSearchResultId = 0;
      } else if (this.activeSearchResultId + 1 === this.results.length) {
        this.activeSearchResultId = null;
      } else {
        this.activeSearchResultId++;
      }

      this.updateQueryWithSearchResult();
    },
    updateQueryWithSearchResult() {
      const hasActiveSearchResult = this.activeSearchResultId !== null;

      this.query = hasActiveSearchResult
        ? this.results[this.activeSearchResultId]
        : this.activeQuery;
    },
    selectSearchResult(activeResultId) {
      this.query = this.results[activeResultId];
      this.updateSearchResults();
      this.toggleSearchResults(false);
    },
    handleClick() {
      this.toggleSearchResults(false);
    },
  },
  watch: {
    query(query) {
      this.$emit('update-search-query', query);
    },
  },
};
</script>

<style scoped></style>
