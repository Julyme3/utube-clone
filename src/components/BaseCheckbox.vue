<template>
  <input
    type="checkbox"
    class="h-5 w-5 cursor-pointer"
    :id="id"
    :value="valueInput"
    v-model="selectedSearchPredictions"
  />
  <label :for="id" class="pl-4 cursor-pointer flex-grow">
    <slot v-if="$slots.default" />
  </label>
</template>

<script>
export default {
  name: 'BaseCheckbox',
  props: {
    id: String,
    modelValue: Array,
    valueInput: String,
  },
  emits: ['update:modelValue'],
  data() {
    return {
      selectedSearchPredictions: this.modelValue,
    };
  },
  watch: {
    selectedSearchPredictions() {
      this.$emit('update:modelValue', [
        ...this.modelValue,
        ...this.selectedSearchPredictions,
      ]);
    },
  },
};
</script>

<style scoped></style>
