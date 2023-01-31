<template>
  <DropdownSettingsHeader title="Choose your language" @back="$emit('close')" />
  <section class="py-2">
    <ul>
      <DropdownSettingsListItem
        v-for="(languageName, languageId) in languages"
        :key="languageId"
        :label="languageName"
        :active="languageId === selectedOptions.language.id"
        @click="selectOption({ id: languageId, text: languageName })"
      />
    </ul>
  </section>
</template>

<script>
import dropdownSubmenu from '../mixins/dropdownSubmenu.js';
export default {
  name: 'TheDropdownSettingsLanguage',
  mixins: [dropdownSubmenu],
  data() {
    return {
      languages: ['English', 'Russian'],
      optionName: 'language',
    };
  },
};
</script>
