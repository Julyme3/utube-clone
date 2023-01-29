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
        <component
          v-if="selectedMenu"
          :is="menu"
          :selected-options="selectedOptions"
          @select-option="selectOption"
          @close="closeMenu"
        />
        <TheDropdownSettingsMain
          v-else
          :menu-items="menuItems"
          @select-menu="selectMenu"
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
      selectedMenu: null,
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
      selectedOptions: {
        theme: {
          id: 0,
          text: 'Device theme',
        },
        language: {
          id: 0,
          text: 'English',
        },
        location: {
          id: 0,
          text: 'United States',
        },
        restrictedMode: {
          enabled: false,
          text: 'Off',
        },
      },
    };
  },
  mounted() {
    window.addEventListener('click', (e) => {
      if (!this.$el.contains(e.target) && this.isOpen) {
        this.close();
      }
    });
  },
  computed: {
    menu() {
      const menuComponentNames = {
        appearance: 'TheDropdownSettingsAppearance',
        language: 'TheDropdownSettingsLanguage',
        location: 'TheDropdownSettingsLocation',
        restricted_mode: 'TheDropdownSettingsRestrictedMode',
      };

      return menuComponentNames[this.selectedMenu.id] ?? null;
    },
    menuItems() {
      return [
        {
          id: 'appearance',
          label: `Appearance: ${this.selectedOptions.theme.text}`,
          icon: 'sun',
          withSubMenu: true,
        },
        {
          id: 'language',
          label: `Language: ${this.selectedOptions.language.text}`,
          icon: 'language',
          withSubMenu: true,
        },
        {
          id: 'location',
          label: `Location: ${this.selectedOptions.location.text}`,
          icon: 'location',
          withSubMenu: true,
        },
        {
          id: 'settings',
          label: 'Settings',
          icon: 'settings',
          withSubMenu: false,
        },
        {
          id: 'your_data_in_youtube',
          label: 'Your data in YouTube',
          icon: 'checkMark',
          withSubMenu: false,
        },
        {
          id: 'help',
          label: 'Help',
          icon: 'questionMark',
          withSubMenu: false,
        },
        {
          id: 'send_feedback',
          label: 'Send feedback',
          icon: 'message',
          withSubMenu: false,
        },
        {
          id: 'keyboard_shortcuts',
          label: 'Keyboard shortcuts',
          icon: 'keyboard',
          withSubMenu: false,
        },
        {
          id: 'restricted_mode',
          label: `Restricted Mode: ${this.selectedOptions.restrictedMode.text}`,
          icon: null,
          withSubMenu: true,
        },
      ];
    },
  },
  watch: {
    isOpen() {
      this.$nextTick(() => this.isOpen && this.$refs.dropdown.focus());
    },
  },
  methods: {
    selectMenu(menu) {
      this.selectedMenu = menu;
      this.$refs.dropdown.focus();
    },
    close() {
      this.isOpen = false;

      setTimeout(() => this.closeMenu, 100);
    },
    open() {
      this.isOpen = true;
    },
    toggle() {
      this.isOpen ? this.close() : this.open();
    },
    selectOption(option) {
      this.selectedOptions[option.name] = option.value;
    },
    closeMenu() {
      this.selectMenu(null);
    },
  },
};
</script>

<style scoped></style>
