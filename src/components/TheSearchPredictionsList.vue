<template>
  <div
    v-for="(label, index) in searchPredictions"
    :key="label"
    class="flex items-center"
  >
    <input
      type="checkbox"
      class="h-5 w-5 cursor-pointer"
      :id="index"
      :value="label"
      v-model="selectedSearchPredictions"
    />
    <label :for="index" class="pl-4 cursor-pointer flex-grow">
      {{ label }}
    </label>
  </div>
</template>

<script>
export default {
  name: 'TheSearchPredictionsList',
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
