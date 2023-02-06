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
      <BaseButton @click="slotProps.close" class="ml-auto">Cancel</BaseButton>
      <BaseButton class="ml-1 text-gray-400 cursor-auto" disabled
        >Report</BaseButton
      >
    </template>
  </BaseModal>
</template>

<script>
import BaseModal from './BaseModal.vue';
import BaseButton from './BaseButton.vue';
import TheSearchPredictionsList from './TheSearchPredictionsList.vue';
export default {
  name: 'TheModalSearchPredictions',
  components: {
    TheSearchPredictionsList,
    BaseModal,
    BaseButton,
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
