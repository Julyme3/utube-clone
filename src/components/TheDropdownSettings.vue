<template>
  <div class="relative">
    <BaseTooltip text="Settings">
      <button @click="toggle" class="relative p-2 focus:outline-none">
        <BaseIcon name="dotsVertical" class="w-5 h-5" />
      </button>
    </BaseTooltip>
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
        @keydown.esc="close"
        :class="dropdownClasses"
      >
        <TheDropdownSettingsMain
          v-if="selectedMenu === 'main'"
          @select-menu="showSelectedMenu"
        />
        <TheDropdownSettingsAppearance
          v-else-if="selectedMenu === 'appearance'"
          @select-menu="showSelectedMenu"
        />
        <TheDropdownSettingsLanguage
          v-else-if="selectedMenu === 'language'"
          @select-menu="showSelectedMenu"
        />
        <TheDropdownSettingsLocation
          v-else-if="selectedMenu === 'location'"
          @select-menu="showSelectedMenu"
        />
        <TheDropdownSettingsRestrictedMode
          v-else-if="selectedMenu === 'restricted_mode'"
          @select-menu="showSelectedMenu"
        />
      </div>
    </transition>
  </div>
</template>

<script>
import BaseIcon from './BaseIcon.vue';
import BaseTooltip from './BaseTooltip.vue';
import TheDropdownSettingsMain from './TheDropdownSettingsMain.vue';
import TheDropdownSettingsAppearance from './TheDropdownSettingsAppearance.vue';
import TheDropdownSettingsLanguage from './TheDropdownSettingsLanguage.vue';
import TheDropdownSettingsLocation from './TheDropdownSettingsLocation.vue';
import TheDropdownSettingsRestrictedMode from './TheDropdownSettingsRestrictedMode.vue';
export default {
  name: 'TheDropdownSettings',
  components: {
    TheDropdownSettingsLocation,
    TheDropdownSettingsMain,
    BaseTooltip,
    BaseIcon,
    TheDropdownSettingsAppearance,
    TheDropdownSettingsLanguage,
    TheDropdownSettingsRestrictedMode,
  },
  data() {
    return {
      selectedMenu: 'main',
      isOpen: false,
      dropdownClasses: [
        'z-10',
        'absolute',
        'top-9',
        '-right-full',
        'sm:right-0',
        'bg-white',
        'w-72',
        'border',
        'border-t-0',
        'focus:outline-none',
      ],
    };
  },
  mounted() {
    window.addEventListener('click', (e) => {
      if (!this.$el.contains(e.target) && this.isOpen) {
        this.close();
      }
    });
  },
  watch: {
    isOpen() {
      this.$nextTick(() => this.isOpen && this.$refs.dropdown.focus());
    },
  },
  methods: {
    showSelectedMenu(selectedMenu) {
      this.selectedMenu = selectedMenu;
      this.$refs.dropdown.focus();
    },
    close() {
      this.isOpen = false;

      setTimeout(() => (this.selectedMenu = 'main'), 100);
    },
    open() {
      this.isOpen = true;
    },
    toggle() {
      this.isOpen ? this.close() : this.open();
    },
  },
};
</script>

<style scoped></style>
