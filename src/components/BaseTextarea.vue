<template>
  <div class="relative">
    <textarea
      v-bind="$attrs"
      @input="updateTextarea"
      placeholder="Provide additional details (optional)"
      class="border rounded-sm pt-2 pb-5 px-2 resize-none w-full focus:outline-none"
    />
    <BaseTextareaCounter>{{ counter }}</BaseTextareaCounter>
  </div>
</template>

<script>
import BaseTextareaCounter from './BaseTextareaCounter.vue';
export default {
  name: 'BaseTextarea',
  components: { BaseTextareaCounter },
  props: {
    modelValue: String,
    limit: Number,
  },
  emits: ['update:modelValue'],
  computed: {
    counter() {
      return `${this.modelValue.length} / ${this.limit}`;
    },
  },
  methods: {
    updateTextarea(e) {
      this.$emit('update:modelValue', e.target.value);
    },
  },
};
</script>

<style scoped></style>
