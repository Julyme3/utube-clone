<template>
  <div class="relative w-full">
    <input
      :value="query"
      :class="classes"
      ref="input"
      @input="updateQuery($event.target.value)"
      @focus="setState(true)"
      @keyup.esc="handleEsc"
      @click.stop="setState(true)"
      @keydown.enter="$emit('enter')"
      type="text"
      placeholder="Search"
    />
    <button
      v-show="query"
      @click="clear"
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
  emits: ['update:query', 'change-state', 'enter'],
  mounted() {
    if (window.innerWidth < 640) {
      this.$refs.input.focus();
    }

    document.addEventListener('keydown', this.handleKeydown);
  },
  beforeUnmount() {
    document.removeEventListener('keydown', this.handleKeydown);
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
    clear() {
      this.updateQuery('');
      this.$refs.input.focus();
    },
    handleEsc() {
      if (this.isActive && this.hasResults) {
        this.setState(false);
      } else {
        this.$refs.input.blur();
      }
    },
    handleKeydown(e) {
      const isInputFocused = this.$refs.input === document.activeElement;

      if (!isInputFocused && e.code === 'Slash') {
        e.preventDefault();

        this.$refs.input.focus();
      }
    },
  },
};
</script>

<style scoped></style>
