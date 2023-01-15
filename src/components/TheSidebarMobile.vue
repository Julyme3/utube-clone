<template>
  <SidebarOverlay>
    <aside class="w-64 max-h-screen overflow-auto bg-white">
      <section class="flex items-center p-4 border-b sticky top-0 bg-white">
        <button class="ml-2 mr-6 focus:outline-none">
          <BaseIcon name="menu" />
        </button>
        <LogoMain />
      </section>
      <SidebarContent />
    </aside>
  </SidebarOverlay>
</template>

<script>
import SidebarOverlay from './SidebarOverlay.vue';
import SidebarContent from './SidebarContent.vue';
import BaseIcon from './BaseIcon.vue';
import LogoMain from './LogoMain.vue';
export default {
  name: 'TheSidebarMobile',
  components: { LogoMain, BaseIcon, SidebarContent, SidebarOverlay },
};
</script>

<style scoped></style>
