<template>
  <input
    type="checkbox"
    class="h-5 w-5 cursor-pointer"
    :id="id"
    v-bind="$attrs"
    @input="updateCheckbox"
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
  methods: {
    updateCheckbox(e) {
      const value = e.target.value;
      let checkboxes = [];

      if (this.modelValue.includes(value)) {
        checkboxes = this.modelValue.filter((el) => el !== value);
      } else {
        checkboxes = [...this.modelValue, value];
      }

      this.$emit('update:modelValue', checkboxes);
    },
  },
};
</script>

<style scoped></style>
