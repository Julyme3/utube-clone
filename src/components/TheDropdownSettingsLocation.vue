<template>
  <DropdownSettingsHeader
    title="Choose your location"
    @back="$emit('select-menu', 'main')"
  />
  <section class="py-2">
    <ul>
      <DropdownSettingsListItem
        v-for="(locationName, locationId) in locations"
        :key="locationId"
        :label="locationName"
        :active="locationId === selectedOptions.locationId"
        @click="selectOption(locationId)"
      />
    </ul>
  </section>
</template>

<script>
import DropdownSettingsHeader from './DropdownSettingsHeader.vue';
import DropdownSettingsListItem from './DropdownSettingsListItem.vue';
export default {
  name: 'TheDropdownSettingsLocation',
  components: {
    DropdownSettingsHeader,
    DropdownSettingsListItem,
  },
  props: ['selectedOptions'],
  emits: ['select-menu', 'select-option'],
  data() {
    return {
      locations: ['United States', 'Russia'],
    };
  },
  methods: {
    selectOption(locationId) {
      this.$emit('select-option', { name: 'locationId', value: locationId });
    },
  },
};
</script>
