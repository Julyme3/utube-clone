<template>
  <TheHeader @toggleSidebar="toggleSidebar" />
  <TheSidebarSmall :isOpen="sidebarState === 'compact'" />
  <TheSidebar :isOpen="sidebarState === 'normal'" />
  <TheSidebarMobile :isOpen="isMobileSidebarOpen" @close="closeMobileSidebar" />
  <TheCategories :isSidebarOpen="sidebarState === 'normal'" />
  <TheVideos :isSidebarOpen="sidebarState === 'normal'" />
</template>
<script>
import TheHeader from './components/TheHeader.vue';
import TheSidebarMobile from './components/TheSidebarMobile.vue';
import TheCategories from './components/TheCategories.vue';
import TheVideos from './components/TheVideos.vue';
import TheSidebar from './components/TheSidebar.vue';
import TheSidebarSmall from './components/TheSidebarSmall.vue';

export default {
  components: {
    TheVideos,
    TheCategories,
    TheSidebarMobile,
    TheHeader,
    TheSidebarSmall,
    TheSidebar,
  },
  data() {
    return {
      isMobileSidebarOpen: false,
      sidebarState: null,
    };
  },
  mounted() {
    const windowWidth = window.innerWidth;
    if (windowWidth >= 768 && windowWidth < 1280) {
      this.sidebarState = 'compact';
    }

    if (windowWidth >= 1280) {
      this.sidebarState = 'normal';
    }
  },
  methods: {
    toggleSidebar() {
      const windowWidth = window.innerWidth;

      if (windowWidth >= 1280) {
        this.sidebarState =
          this.sidebarState === 'compact' ? 'normal' : 'compact';
      } else {
        this.openMobileSidebar();
      }
    },
    openMobileSidebar() {
      this.isMobileSidebarOpen = true;
    },
    closeMobileSidebar() {
      this.isMobileSidebarOpen = false;
    },
  },
};
</script>
