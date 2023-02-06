<template>
  <div
    v-for="(label, index) in searchPredictions"
    :key="label"
    class="flex items-center"
  >
    <BaseCheckbox
      :id="`search-prediction-${index}`"
      v-model="selectedSearchPredictions"
      :valueInput="label"
    >
      {{ label }}
    </BaseCheckbox>
  </div>
</template>

<script>
import BaseCheckbox from './BaseCheckbox.vue';
export default {
  name: 'TheSearchPredictionsList',
  components: {
    BaseCheckbox,
  },
  props: {
    searchPredictions: Array,
    modelValue: Array,
  },
  emits: ['update:modelValue'],
  data() {
    return {
      selectedSearchPredictions: this.modelValue,
    };
  },
  watch: {
    selectedSearchPredictions() {
      this.$emit('update:modelValue', this.selectedSearchPredictions);
    },
  },
};
</script>

<style scoped></style>
