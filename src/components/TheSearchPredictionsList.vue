<template>
  <div
    v-for="(label, index) in searchPredictions"
    :key="label"
    class="flex items-center"
  >
    <BaseCheckbox
      :id="`search-prediction-${index}`"
      v-model="selectedSearchPredictions"
      :value="label"
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
  computed: {
    selectedSearchPredictions: {
      get() {
        return this.modelValue;
      },
      set(value) {
        this.$emit('update:modelValue', value);
      },
    },
  },
};
</script>

<style scoped></style>
