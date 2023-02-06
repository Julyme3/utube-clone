<template>
  <BaseModal class="md:w-4/5 max-w-2xl">
    <p class="text-base text-black tracking-wide">Report search predictions</p>
    <div class="space-y-3 text-black text-sm mt-5">
      <TheSearchPredictionsList
        :search-predictions="searchPredictions"
        v-model="selectedSearchPredictions"
      />
    </div>
    <template #footer="slotProps">
      <button
        @click="slotProps.close"
        class="uppercase text-sm font-medium tracking-wider py-2.5 px-4 ml-auto mr-1 focus:outline-none"
      >
        Cancel
      </button>
      <button
        class="uppercase text-sm font-medium tracking-wider py-2.5 px-4 ml-1 mr-1 focus:outline-none text-gray-400 cursor-auto"
        disabled
      >
        Report
      </button>
    </template>
  </BaseModal>
</template>

<script>
import BaseModal from './BaseModal.vue';
import TheSearchPredictionsList from './TheSearchPredictionsList.vue';
export default {
  name: 'TheModalSearchPredictions',
  components: {
    TheSearchPredictionsList,
    BaseModal,
  },
  props: {
    searchPredictions: Array,
  },
  data() {
    return {
      selectedSearchPredictions: [],
    };
  },
};
</script>
