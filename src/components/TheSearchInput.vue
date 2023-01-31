<template>
  <div class="relative w-full">
    <input
      :value="query"
      :class="classes"
      ref="input"
      @input="updateQuery($event.target.value)"
      @focus="setState(true)"
      @blur="setState(false)"
      @keyup.esc="handleEsc"
      @click="setState(true)"
      type="text"
      placeholder="Search"
    />
    <button
      v-show="query"
      @click="updateQuery('')"
      class="absolute top-0 right-0 h-full px-3 focus:outline-none"
    >
      <BaseIcon name="x" class="w-5 w-5" />
    </button>
  </div>
</template>

<script>
import BaseIcon from './BaseIcon.vue';
export default {
  name: 'TheSearchInput',
  components: {
    BaseIcon,
  },
  props: ['query', 'hasResults'],
  emits: ['update:query', 'change-state'],
  mounted() {
    if (window.innerWidth < 640) {
      this.$el.focus();
    }
  },
  data() {
    return {
      isActive: false,
      classes: [
        'w-full',
        'h-full',
        'px-3',
        'shadow-inner',
        'rounded-bl-sm',
        'rounded-tl-sm',
        'border',
        'border-gray-300',
        'focus:border-blue-700',
        'focus:outline-none',
      ],
    };
  },
  methods: {
    updateQuery(query) {
      this.$emit('update:query', query);
      this.setState(true);
    },
    setState(state) {
      this.isActive = state;
      this.$emit('change-state', state);
    },
    handleEsc() {
      if (this.isActive && this.hasResults) {
        this.setState(false);
      } else {
        this.$refs.input.blur();
      }
    },
  },
};
</script>

<style scoped></style>
