<template>
  <DropdownSettingsHeader title="Choose your location" @back="$emit('close')" />
  <section class="py-2">
    <ul>
      <DropdownSettingsListItem
        v-for="(locationName, locationId) in locations"
        :key="locationId"
        :label="locationName"
        :active="locationId === selectedOptions.location.id"
        @click="selectOption({ id: locationId, text: locationName })"
      />
    </ul>
  </section>
</template>

<script>
import dropdownSubmenu from '../mixins/dropdownSubmenu';

export default {
  name: 'TheDropdownSettingsLocation',
  mixins: [dropdownSubmenu],
  data() {
    return {
      locations: ['United States', 'Russia'],
      optionName: 'location',
    };
  },
};
</script>
