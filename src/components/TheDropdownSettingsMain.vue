<template>
  <section class="py-2 border-b">
    <ul>
      <DropdownSettingsListItem
        v-for="listItem in listItems.slice(0, listItems.length - 1)"
        :key="listItem.label"
        :label="listItem.label"
        :icon="listItem.icon"
        :withSubMenu="listItem.withSubMenu"
        @click.stop="$emit('select-menu', listItem.id)"
      />
    </ul>
  </section>
  <section class="py-2">
    <ul>
      <DropdownSettingsListItem
        :label="lastListItem.label"
        :icon="lastListItem.icon"
        :withSubMenu="lastListItem.withSubMenu"
        @click.stop="$emit('select-menu', lastListItem.id)"
      />
    </ul>
  </section>
</template>

<script>
import DropdownSettingsListItem from './DropdownSettingsListItem.vue';
export default {
  name: 'TheDropdownSettingsMain',
  components: {
    DropdownSettingsListItem,
  },
  emits: ['select-menu'],
  data() {
    return {
      listItems: [
        {
          id: 'appearance',
          label: 'Appearance: Light',
          icon: 'sun',
          withSubMenu: true,
        },
        {
          id: 'language',
          label: 'Language: English',
          icon: 'language',
          withSubMenu: true,
        },
        {
          id: 'location',
          label: 'Location: Ukraine',
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
          label: 'Restricted Mode: Off',
          icon: null,
          withSubMenu: true,
        },
      ],
    };
  },
  computed: {
    lastListItem() {
      return this.listItems[this.listItems.length - 1];
    },
  },
};
</script>

<style scoped></style>
