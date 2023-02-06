<template>
  <textarea
    v-bind="$attrs"
    v-model="textValue"
    placeholder="Provide additional details (optional)"
    class="border rounded-sm pt-2 pb-5 px-2 resize-none w-full focus:outline-none"
  />
</template>

<script>
export default {
  name: 'BaseTextarea',
  props: {
    modelValue: String,
  },
  emits: ['update:modelValue'],
  data() {
    return {
      textValue: this.modelValue,
    };
  },
  watch: {
    textValue() {
      this.$emit('update:modelValue', this.textValue);
    },
  },
};
</script>

<style scoped></style>
