<template>
  <section class="py-2 border-b">
    <ul>
      <DropdownSettingsListItem
        v-for="menuItem in menuItems.slice(0, menuItems.length - 1)"
        :key="menuItem.label"
        :label="menuItem.label"
        :icon="menuItem.icon"
        :withSubMenu="menuItem.withSubMenu"
        @click.stop="selectMenu(menuItem)"
      />
    </ul>
  </section>
  <section class="py-2">
    <ul>
      <DropdownSettingsListItem
        :label="lastMenuItem.label"
        :icon="lastMenuItem.icon"
        :withSubMenu="lastMenuItem.withSubMenu"
        @click.stop="selectMenu(lastMenuItem)"
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
  props: ['menuItems'],
  emits: ['select-menu'],
  computed: {
    lastMenuItem() {
      return this.menuItems[this.menuItems.length - 1];
    },
  },
  methods: {
    selectMenu(menuItem) {
      if (menuItem.withSubMenu) {
        this.$emit('select-menu', menuItem);
      }
    },
  },
};
</script>

<style scoped></style>
