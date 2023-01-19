<template>
  <div class="relative -mt-1 ml-auto">
    <transition
      enter-active-class="transition ease-out duration-100"
      enter-from-class="transition opacity-0 scale-95"
      enter-to-class="transform opacity-100 scale-100"
      leave-active-class="transition ease-in duration-75"
      leave-from-class="transform opacity-100 scale-100"
      leave-to-class="transform opacity-0 scale-95"
    >
      <div
        v-show="isOpen"
        ref="dropdown"
        tabindex="-1"
        @keydown.esc="isOpen = false"
        class="absolute top-9 -right-full sm:right-0 bg-white w-48 rounded shadow focus:outline-none"
      >
        <section class="py-2">
          <ul>
            <VideoItemDropdownListItem label="Add to queue" icon="altMenu3" />
          </ul>
        </section>
      </div>
    </transition>
    <button
      @click="isOpen = !isOpen"
      class="-mt-1 ml-auto p-1 opacity-0 group-hover:opacity-100 text-gray-500 hover:text-gray-700 focus:outline-none"
    >
      <BaseIcon name="dotsVertical" />
    </button>
  </div>
</template>

<script>
import BaseIcon from './BaseIcon.vue';
import VideoItemDropdownListItem from './VideoItemDropdownListItem.vue';
export default {
  name: 'VideoItemDropdown',
  components: {
    BaseIcon,
    VideoItemDropdownListItem,
  },
  data() {
    return {
      isOpen: false,
    };
  },
  mounted() {
    window.addEventListener('click', (e) => {
      if (!this.$el.contains(e.target) && this.isOpen) {
        this.isOpen = false;
      }
    });
  },
  watch: {
    isOpen() {
      this.$nextTick(() => this.isOpen && this.$refs.dropdown.focus());
    },
  },
};
</script>

<style scoped></style>
