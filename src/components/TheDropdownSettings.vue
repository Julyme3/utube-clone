<template>
  <div class="relative">
    <button @click="isOpen = !isOpen" class="relative p-2 focus:outline-none">
      <BaseIcon name="dotsVertical" class="w-5 h-5" />
    </button>
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
        class="absolute top-9 -right-full sm:right-0 bg-white w-72 border border-t-0"
      >
        <section class="py-2 border-b">
          <ul>
            <DropdownSettingsListItem
              v-for="listItem in listItems.slice(0, listItems.length - 1)"
              :key="listItem.label"
              :label="listItem.label"
              :icon="listItem.icon"
              :withSubMenu="listItem.withSubMenu"
            />
          </ul>
        </section>
        <section class="py-2">
          <ul>
            <DropdownSettingsListItem
              :label="lastListItem.label"
              :icon="lastListItem.icon"
              :withSubMenu="lastListItem.withSubMenu"
            />
          </ul>
        </section>
      </div>
    </transition>
  </div>
</template>

<script>
import BaseIcon from './BaseIcon.vue';
import DropdownSettingsListItem from './DropdownSettingsListItem.vue';
export default {
  name: 'TheDropdownSettings',
  components: { DropdownSettingsListItem, BaseIcon },
  data() {
    return {
      listItems: [
        {
          label: 'Appearance: Light',
          icon: 'sun',
          withSubMenu: true,
        },
        {
          label: 'Language: English',
          icon: 'language',
          withSubMenu: true,
        },
        {
          label: 'Location: Ukraine',
          icon: 'location',
          withSubMenu: true,
        },
        {
          label: 'Settings',
          icon: 'settings',
          withSubMenu: false,
        },
        {
          label: 'Your data in YouTube',
          icon: 'checkMark',
          withSubMenu: false,
        },
        {
          label: 'Help',
          icon: 'questionMark',
          withSubMenu: false,
        },
        {
          label: 'Send feedback',
          icon: 'message',
          withSubMenu: false,
        },
        {
          label: 'Keyboard shortcuts',
          icon: 'keyboard',
          withSubMenu: false,
        },
        {
          label: 'Restricted Mode: Off',
          icon: null,
          withSubMenu: true,
        },
      ],
      isOpen: false,
    };
  },
  computed: {
    lastListItem() {
      return this.listItems[this.listItems.length - 1];
    },
  },
  mounted() {
    window.addEventListener('click', (e) => {
      if (!this.$el.contains(e.target) && this.isOpen) {
        this.isOpen = false;
      }
    });
  },
};
</script>

<style scoped></style>
