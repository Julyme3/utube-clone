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
        :active="themeId === selectedThemeId"
        @click="selectedThemeId = themeId"
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
  emits: ['select-menu'],
  data() {
    return {
      themes: ['Use device theme', 'Dark theme', 'Light theme'],
      selectedThemeId: 0,
    };
  },
};
</script>

<style scoped></style>
