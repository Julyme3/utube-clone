<template>
  <div class="fixed w-full z-30">
    <TheHeader @toggleSidebar="toggleSidebar" />
    <TheCategories :isSidebarOpen="isSidebarOpen" />
  </div>
  <TheSidebarCompact v-if="isCompactSidebarOpen" />
  <TheSidebar v-if="isSidebarOpen" />
  <TheSidebarMobile :isOpen="isMobileSidebarOpen" @close="closeMobileSidebar" />
  <TheVideos :isSidebarOpen="isSidebarOpen" />
</template>
<script>
import TheHeader from './components/TheHeader.vue';
import TheSidebarMobile from './components/TheSidebarMobile.vue';
import TheCategories from './components/TheCategories.vue';
import TheVideos from './components/TheVideos.vue';
import TheSidebar from './components/TheSidebar.vue';
import TheSidebarCompact from './components/TheSidebarCompact.vue';

export default {
  components: {
    TheVideos,
    TheCategories,
    TheSidebarMobile,
    TheHeader,
    TheSidebarCompact,
    TheSidebar,
  },
  data() {
    return {
      isMobileSidebarOpen: false,
      isCompactSidebarActive: false,
      isSidebarOpen: false,
      isCompactSidebarOpen: false,
    };
  },
  mounted() {
    this.onResize();

    window.addEventListener('resize', this.onResize);
  },
  methods: {
    onResize() {
      const windowWidth = window.innerWidth;

      if (windowWidth < 768) {
        this.isCompactSidebarOpen = false;
        this.isSidebarOpen = false;
      } else if (windowWidth < 1280) {
        this.isCompactSidebarOpen = true;
        this.isSidebarOpen = false;
      } else {
        this.isCompactSidebarOpen = this.isCompactSidebarActive;
        this.isSidebarOpen = !this.isCompactSidebarActive;
        this.isMobileSidebarOpen = false;
      }
    },
    toggleSidebar() {
      const windowWidth = window.innerWidth;

      if (windowWidth >= 1280) {
        this.isCompactSidebarActive = !this.isCompactSidebarActive;

        this.onResize();
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
