<template>
  <section class="py-2 border-b">
    <ul>
      <DropdownSettingsListItem
        v-for="listItem in listItems.slice(0, listItems.length - 1)"
        :key="listItem.label"
        :label="listItem.label"
        :icon="listItem.icon"
        :withSubMenu="listItem.withSubMenu"
        @click.stop="$emit('select-menu', 'appearance')"
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
