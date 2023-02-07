<template>
  <input
    type="radio"
    class="h-5 w-5 cursor-pointer"
    :id="id"
    v-bind="$attrs"
    @input="updateRadio"
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
  methods: {
    updateRadio(e) {
      this.$emit('update:modelValue', e.target.value);
    },
  },
};
</script>

<style scoped></style>
