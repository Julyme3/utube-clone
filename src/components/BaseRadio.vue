<template>
  <input
    type="radio"
    class="h-5 w-5 cursor-pointer"
    :id="id"
    v-bind="$attrs"
    v-model="selectedValue"
  />
  <label v-if="$slots.default" :for="id" class="pl-4 cursor-pointer flex-grow"
    ><slot
  /></label>
</template>

<script>
export default {
  name: 'BaseRadio',
  props: {
    id: String,
    modelValue: String,
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
