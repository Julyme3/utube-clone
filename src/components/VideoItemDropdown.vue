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
        :class="dropdownClasses"
      >
        <section class="py-2">
          <ul>
            <VideoItemDropdownListItem label="Add to queue" icon="altMenu3" />
          </ul>
        </section>
      </div>
    </transition>
    <button @click="toggle" :class="buttonClasses">
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
      positionClasses: [],
    };
  },
  computed: {
    buttonClasses() {
      return [
        'p-1',
        'text-gray-500',
        'hover:text-gray-700',
        'focus:outline-none',
        this.isOpen ? 'opacity-100' : 'opacity-0',
        'group-hover:opacity-100',
      ];
    },
    dropdownClasses() {
      return [
        'z-10',
        'absolute',
        'bg-white',
        'w-48',
        'rounded',
        'shadow',
        'focus:outline-none',
        ...this.positionClasses,
      ];
    },
  },
  mounted() {
    window.addEventListener('click', (e) => {
      if (!this.$el.contains(e.target) && this.isOpen) {
        this.isOpen = false;
      }
    });
  },
  methods: {
    toggle(e) {
      this.isOpen = !this.isOpen;

      if (this.isOpen) {
        this.$nextTick(
          () => (this.positionClasses = this.getPositionClasses(e))
        );
      }
    },
    getPositionClasses(e) {
      return [
        this.getTopClasses(e),
        this.getBottomClass(e),
        this.getRightClasses(e),
        this.getLeftClass(e),
      ];
    },
    getTopClasses(e) {
      const clickCoordY = e.clientY;
      const dropdownHeight = this.$refs.dropdown.offsetHeight;
      const buttonHeight = e.currentTarget.offsetHeight;
      const windowHeight = window.innerHeight;

      if (windowHeight - clickCoordY < dropdownHeight) {
        return 'top-auto';
      }

      if (windowHeight - clickCoordY < dropdownHeight + buttonHeight) {
        return 'top-0';
      }

      return 'top-9';
    },
    getBottomClass(event) {
      const clickCoordY = event.clientY;
      const dropdownHeight = this.$refs.dropdown.offsetHeight;
      if (window.innerHeight - clickCoordY < dropdownHeight) {
        return 'bottom-9';
      }
      return 'buttom-auto';
    },
    getRightClasses(e) {
      const clickCoordX = e.clientX;
      const clickCoordY = e.clientY;
      const dropdownHeight = this.$refs.dropdown.offsetHeight;
      const dropdownWidth = this.$refs.dropdown.offsetWidth;
      const buttonHeight = e.currentTarget.offsetHeight;
      const windowWidth = window.innerWidth;
      const windowHeight = window.innerHeight;

      if (windowWidth - clickCoordX > dropdownWidth) {
        return 'right-auto';
      }

      if (windowHeight - clickCoordY > dropdownHeight + buttonHeight) {
        return 'right-0';
      }

      if (windowHeight - clickCoordY > dropdownHeight) {
        return 'right-8';
      }

      return 'right-0';
    },
    getLeftClass(e) {
      const clickCoordX = e.clientX;
      const clickCoordY = e.clientY;
      const buttonHeight = e.currentTarget.offsetHeight;
      const dropdownWidth = this.$refs.dropdown.offsetWidth;
      const dropdownHeight = this.$refs.dropdown.offsetHeight;
      const windowWidth = window.innerWidth;

      if (windowWidth - clickCoordX < dropdownWidth) {
        return 'left-auto';
      }

      if (windowWidth - clickCoordY < dropdownHeight) {
        return 'left-auto';
      }

      if (windowWidth - clickCoordY > dropdownHeight + buttonHeight) {
        return 'left-auto';
      }

      return 'left-8';
    },
  },
  watch: {
    isOpen() {
      this.$nextTick(() => this.isOpen && this.$refs.dropdown.focus());
    },
  },
};
</script>

<style scoped></style>
