<template>
  <div class="space-y-3 text-black text-sm mt-5">
    <div
      v-for="(label, index) in searchPredictionCategories"
      :key="label"
      class="flex items-center"
    >
      <input
        type="radio"
        class="h-5 w-5 cursor-pointer"
        :id="`search-prediction-category-${index}`"
        :value="label"
        v-model="selectedValue"
      />
      <label
        :for="`search-prediction-category-${index}`"
        class="pl-4 cursor-pointer flex-grow"
        >{{ label }}</label
      >
    </div>
  </div>
</template>

<script>
export default {
  name: 'TheSearchPredictionCategories',
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
