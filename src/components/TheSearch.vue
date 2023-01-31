<template>
  <div class="flex w-full mr-2">
    <div class="relative flex w-full">
      <TheSearchInput
        v-model:query="query"
        :has-results="results.length"
        @change-state="toggleSearchResults"
        @keyup.up="handlePreviousSearchResult"
        @keyup.down="handleNextSearchResult"
      />
      <TheSearchResults
        v-show="isSearchResultsShown"
        :results="results"
        :activeResultId="activeSearchResultId"
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
      query: this.searchQuery,
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
  computed: {
    results() {
      if (!this.query) {
        return [];
      }

      return this.keywords.filter((result) => {
        return result.includes(this.trimmedQuery);
      });
    },
    trimmedQuery() {
      return this.query.replace(/\s+/g, ' ');
    },
  },
  methods: {
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
    },
    makeNextSearchResultActive() {
      if (this.activeSearchResultId === null) {
        this.activeSearchResultId = 0;
      } else if (this.activeSearchResultId + 1 === this.results.length) {
        this.activeSearchResultId = null;
      } else {
        this.activeSearchResultId++;
      }
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
