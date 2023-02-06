<template>
  <BaseModal class="md:w-4/5 max-w-2xl">
    <p class="text-base text-black tracking-wide">Report search predictions</p>
    <div class="space-y-3 text-black text-sm mt-5">
      <TheSearchPredictionsList
        :search-predictions="searchPredictions"
        v-model="selectedSearchPredictions"
      />
    </div>
    <p class="text-xs text-gray-600 mt-5">The selected predictions are:</p>
    <TheSearchPredictionCategories
      :search-prediction-categories="searchPredictionCategories"
      v-model="selectedSearchPredictionCategory"
    />
    <div class="text-black text-sm mt-6">
      <BaseTextarea v-model="searchPredictionDetails" />
    </div>
    <template #footer="slotProps">
      <BaseButton @click="slotProps.close" class="ml-auto">Cancel</BaseButton>
      <BaseButton class="ml-1 text-gray-400 cursor-auto" disabled
        >Report</BaseButton
      >
    </template>
  </BaseModal>
</template>

<script>
import BaseModal from './BaseModal.vue';
import BaseTextarea from './BaseTextarea.vue';
import BaseButton from './BaseButton.vue';
import TheSearchPredictionsList from './TheSearchPredictionsList.vue';
import TheSearchPredictionCategories from './TheSearchPredictionCategories.vue';
export default {
  name: 'TheModalSearchPredictions',
  components: {
    TheSearchPredictionCategories,
    TheSearchPredictionsList,
    BaseModal,
    BaseButton,
    BaseTextarea,
  },
  props: {
    searchPredictions: Array,
  },
  data() {
    return {
      searchPredictionDetails: '',
      selectedSearchPredictions: [],
      selectedSearchPredictionCategory: null,
      searchPredictionCategories: [
        'Hateful',
        'Sexually Explicit',
        'Violent',
        'Dangerous and harmful activity',
        'Other',
      ],
    };
  },
};
</script>
