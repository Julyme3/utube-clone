<template>
  <div class="space-y-3 text-black text-sm mt-5">
    <div
      v-for="(label, index) in searchPredictionCategories"
      :key="label"
      class="flex items-center"
    >
      <BaseRadio
        :id="`search-prediction-category-${index}`"
        :value="label"
        v-model="selectedValue"
        name="search-prediction-category"
        >{{ label }}</BaseRadio
      >
    </div>
  </div>
</template>

<script>
import BaseRadio from './BaseRadio.vue';
export default {
  name: 'TheSearchPredictionCategories',
  components: { BaseRadio },
  props: {
    searchPredictionCategories: Array,
    modelValue: null | String,
  },
  emits: ['update:modelValue'],
  data() {
    return {
      selectedValue: this.modelValue,
    };
  },
  watch: {
    selectedValue() {
      this.$emit('update:modelValue', this.selectedValue);
    },
  },
};
</script>

<style scoped></style>
