<template>
  <input
    type="checkbox"
    class="h-5 w-5 cursor-pointer"
    :id="id"
    v-bind="$attrs"
    v-model="localState"
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
  },
  emits: ['update:modelValue'],
  computed: {
    localState: {
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
