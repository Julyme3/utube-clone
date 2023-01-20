<template>
  <div class="fixed bg-white w-full h-14 p-3 z-10 flex">
    <BaseTooltip text="Back">
      <button class="p-2 focus:outline-none">
        <BaseIcon name="arrowLeft" class="w-5 h-5" />
      </button>
    </BaseTooltip>
    <TheSearch />
    <BaseTooltip text="Search with your voice">
      <button class="p-2 focus:outline-none">
        <BaseIcon name="microphone" class="w-5 h-5" />
      </button>
    </BaseTooltip>
  </div>
</template>

<script>
import BaseTooltip from './BaseTooltip.vue';
import BaseIcon from './BaseIcon.vue';
import TheSearch from './TheSearch.vue';
export default {
  name: 'TheSearchMobile',
  components: {
    BaseIcon,
    BaseTooltip,
    TheSearch,
  },
};
</script>

<style scoped></style>
