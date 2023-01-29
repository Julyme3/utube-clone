<template>
  <DropdownSettingsHeader
    title="Restricted Mode"
    @back="$emit('select-menu', 'main')"
  />
  <section class="px-3 py-4 space-y-4 text-black text-sm">
    <p>
      This helps hide potentially mature videos. No filter is 100% accurate.
    </p>
    <p>This setting only applies to this browser.</p>
    <div class="text-gray-600 font-semibold flex items-center">
      <label for="restrictedMode" class="uppercase mr-2"
        >Activate restricted mode</label
      >
      <input
        id="restrictedMode"
        type="checkbox"
        :checked="selectedOptions.restrictedMode.enabled"
        @input="selectOption"
      />
    </div>
  </section>
</template>

<script>
import DropdownSettingsHeader from './DropdownSettingsHeader.vue';
export default {
  name: 'TheDropdownSettingsRestrictedMode',
  components: {
    DropdownSettingsHeader,
  },
  props: ['selectedOptions'],
  emits: ['select-menu', 'select-option'],
  methods: {
    selectOption(e) {
      const enabled = e.target.checked;
      const text = enabled ? 'On' : 'Off';

      this.$emit('select-option', {
        name: 'restrictedMode',
        value: {
          enabled,
          text,
        },
      });
    },
  },
};
</script>
