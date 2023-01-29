<template>
  <DropdownSettingsHeader
    title="Appearance"
    @back="$emit('select-menu', 'main')"
  />
  <section class="py-2 border-b">
    <div class="text-gray-500 text-xs p-3">
      Setting applies to this browser only
    </div>
    <ul>
      <DropdownSettingsListItem
        v-for="(themeName, themeId) in themes.slice(0, 8)"
        :key="themeId"
        :label="themeName"
        :active="themeId === selectedOptions.themeId"
        @click="selectOption(themeId)"
      />
    </ul>
  </section>
</template>

<script>
import DropdownSettingsListItem from './DropdownSettingsListItem.vue';
import BaseIcon from './BaseIcon.vue';
import DropdownSettingsHeader from './DropdownSettingsHeader.vue';
export default {
  name: 'TheDropdownSettingsAppearance',
  components: {
    DropdownSettingsHeader,
    DropdownSettingsListItem,
    BaseIcon,
  },
  props: ['selectedOptions'],
  emits: ['select-menu', 'select-option'],
  data() {
    return {
      themes: ['Use device theme', 'Dark theme', 'Light theme'],
    };
  },
  methods: {
    selectOption(themeId) {
      this.$emit('select-option', { name: 'themeId', value: themeId });
    },
  },
};
</script>

<style scoped></style>
