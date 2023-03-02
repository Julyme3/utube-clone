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
  computed: {
    selectedValue: {
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
