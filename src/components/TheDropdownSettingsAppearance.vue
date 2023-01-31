<template>
  <DropdownSettingsHeader title="Appearance" @back="$emit('close')" />
  <section class="py-2 border-b">
    <div class="text-gray-500 text-xs p-3">
      Setting applies to this browser only
    </div>
    <ul>
      <DropdownSettingsListItem
        v-for="(themeName, themeId) in themes.slice(0, 8)"
        :key="themeId"
        :label="themeName"
        :active="themeId === selectedOptions.theme.id"
        @click="selectOption({ id: themeId, text: themeName })"
      />
    </ul>
  </section>
</template>

<script>
import dropdownSubmenu from '../mixins/dropdownSubmenu.js';
import BaseIcon from './BaseIcon.vue';
export default {
  name: 'TheDropdownSettingsAppearance',
  components: {
    BaseIcon,
  },
  mixins: [dropdownSubmenu],
  data() {
    return {
      themes: ['Device theme', 'Dark theme', 'Light theme'],
      optionName: 'theme',
    };
  },
};
</script>

<style scoped></style>
